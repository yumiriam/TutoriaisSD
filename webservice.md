> Usamos o material do professor de Web Service com NetBeans

# Algumas informações úteis

## Cliente Android (com ksoap2)

NAMESPACE
	Namespace é o targetNamespace no WSDL.

URL
	A URL do WSDL. Seu valor é o atributo location do elemento soap:address referente a um elemento port em um WSDL. A não ser que o serviço da Web também esteja hospedado no dispositivo Android, o nome do host não deve ser especificado como localhost, porque o aplicativo executa no dispositivo Android, enquanto o serviço da Web está hospedado no servidor localhost . Especifique o nome de host como o endereço IP do servidor que hospeda o serviço da Web.

METHOD_NAME
	Nome da operação do serviço da Web, que pode ser obtido a partir do WSDL.

SOAP_ACTION
	NAMESPACE+METHOD_NAME especificado com um literal de cadeia de caractere.

