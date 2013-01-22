ORB (Object Request Broker)

POA (Portable Object Adapter)
	detalhes de como os objetos servidores devem ser implementados e registradps no sistema
	torna o código do lado servidor portável entre ORBs
	para ativar o objeto servidor e torná-lo disponível aos clientes, deve-se registrá-lo com um POA
	
IOR (Interoperable Object Reference)

1. Definindo a interface do objeto em IDL

> <myobject>.idl
interface MyObject {
    # lista de assinaturas de operações
    {<returnType> <operationName>(<[in|out]> <paramType> <paramName>)}
};

# a interface é definida no namespace IDL global
# evitar esta prática usando nomes de módulos (module)

2. Acesso à um objeto CORBA

servant (objeto servidor) é a implementação do objeto CORBA
	em CORBA, todo objeto herda de CORBA::Object
object reference (referência) é o meio pelo qual se acessa o objeto
	em CORBA, CORBA::Object_ptr
o código cliente lida apenas com a referência
a implementação do objeto pode lidar com ambos

3. Gerando o código do stub

> bash
$ omniidl -bcxx echo.idl

# omniidl é o compilador IDL
# com esse argumento produz o mapeamento C++ da interface
# são dois arquivos stub: um cabeçalho e um arquivo fonte C++
# com extensões .hh e .cc

http://omniorb.sourceforge.net/omni40/omniORB/omniORB005.html

o mapeamento em C++:

object reference -> MyObject_ptr

funções-membro estáticas da classe MyObject:
_nil() retorna uma referência nula (nil object reference) pra interface MyObject
	sempre verdadeiro:
		CORBA::Boolean true_result = CORBA::is_nil(Echo::_nil());
_duplicate()
	retorna uma nova referência pra interface MyObject
_narrow()
	toma um argumento do tipo CORBA::Object_ptr e retorna uma nova referência pra interface MyObject
	pode lançar as as exceções de sistema: COMM_FAILURE ou OBJECT_NOT_EXIST

em CORBA, CORBA::release() desaloca a *referência*:
	CORBA::release(CORBA::Object_ptr obj)
em CORBA, _is_equivalent() verifica se duas referências são equivalentes:
	CORBA::Boolean true_result = A->_is_equivalent(B);
	
MyObject_var cuida da alocação e desalocação automaticamente quando as variáveis são reatribuídas
	pode ser usada em conjunto com MyObject_ptr pra acessar o objeto
	aloca objeto no heap

4. Implementação do objeto servidor

POA: pra cada interface é gerado um esqueleto (skeleton)

classe de implementação para prover a implementação do servidor:
	deve herdar da classe do esqueleto
	deve implementar todas as funções abstratas definidas na classe esqueleto
	
pontos importantes:
	armazenamento
	multi-threading
	contador de referência
		libera MyObject_i quando nenhuma referência a ele está sendo feita na aplicação ou no POA
	instanciação
		sempre usando new

5. Implementação do código do cliente

procurar usar as variáveis automáticas (T_ptr em vez de T_var)
	maximiza performance

6. Ligação entre cliente e servidor (implementação) 

CORBA::ORB_init() inicializa o ORB, 3o argumento especifíca o ORB ('omniORB4')
	lança a exceção CORBA::INITIALIZE

orb->resolve_initial_references() obtém o POA Root, com o argumento 'RootPOA'
	retorna um objeto CORBA::Object
	
poa->activate_object() ativa o objeto servidor
	retorna um objeto PortableServer::ObjectId*

PortableServer::POAManager_var pman = poa->the_POAManager();
pman->activate();
	estado inicial do POA é holding, deve ser ativado com o POA Manager

passando referências entre dois espaços de endereço:
	a. versão stringified da referência
		object_to_string() retorna a string da referência
		string_to_object() retorna a referência da string
	b. serviço de nomes (Naming Service)
		componentes de nome: '<id>.<kind>/MyObject.Object'
