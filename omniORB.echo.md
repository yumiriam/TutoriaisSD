# defines the object interface in IDL

>  echo.idl

	interface Echo {
		string echoString(in string mesg);
	};

# use the IDL compiler to generate the stub code

> bash

	$ omniidl -bcxx echo.idl

> omniidl is the IDL compiler
> it produces the C++ mapping of the interface
> which consists by two stub files: a C++ header file and a C++ source file
> with .hh and .cc extensions

# provide the servant object implementation

> example

	class Echo_i : public POA_Echo,
		    public PortableServer::RefCountServantBase
	{
	public:
	  inline Echo_i() {}
	  virtual ~Echo_i() {}
	  virtual char* echoString(const char* mesg);
	};

	char* Echo_i::echoString(const char* mesg)
	{
	  return CORBA::string_dup(mesg);
	}

# write the client code

> example

	 1  void
	 2  hello(CORBA::Object_ptr obj)
	 3  {
	 4    Echo_var e = Echo::_narrow(obj);
	 5
	 6    if (CORBA::is_nil(e)) {
	 7      cerr << "cannot invoke on a nil object reference."
	 8           << endl;
	 9      return;
	10    }
	11
	12    CORBA::String_var src = (const char*) "Hello!";
	13    CORBA::String_var dest;
	14
	15    dest = e->echoString(src);
	16
	17    cerr << "I said,\"" << src << "\"."
	18         << " The Object said,\"" << dest <<"\"" << endl;
	19  }

# link the client and implementation

> same address space

	 1  int
	 2  main(int argc, char **argv)
	 3  {
	 4    CORBA::ORB_ptr orb = CORBA::ORB_init(argc,argv,"omniORB4");
	 5
	 6    CORBA::Object_var       obj = orb->resolve_initial_references("RootPOA");
	 7    PortableServer::POA_var poa = PortableServer::POA::_narrow(obj);
	 8
	 9    Echo_i *myecho = new Echo_i();
	10    PortableServer::ObjectId_var myechoid = poa->activate_object(myecho);
	11
	12    Echo_var myechoref = myecho->_this();
	13    myecho->_remove_ref();
	14
	15    PortableServer::POAManager_var pman = poa->the_POAManager();
	16    pman->activate();
	17
	18    hello(myechoref);
	19
	20    orb->destroy();
	21    return 0;
	22  }

> different address spaces : stringfied

	 1  int main(int argc, char** argv)
	 2  {
	 3    CORBA::ORB_var orb = CORBA::ORB_init(argc, argv);
	 4
	 5    CORBA::Object_var       obj = orb->resolve_initial_references("RootPOA");
	 6    PortableServer::POA_var poa = PortableServer::POA::_narrow(obj);
	 7
	 8    Echo_i* myecho = new Echo_i();
	 9
	10    PortableServer::ObjectId_var myechoid = poa->activate_object(myecho);
	11
	12    obj = myecho->_this();
	13    CORBA::String_var sior(orb->object_to_string(obj));
	14    cerr << "'" << (char*)sior << "'" << endl;
	15
	16    myecho->_remove_ref();
	17
	18    PortableServer::POAManager_var pman = poa->the_POAManager();
	19    pman->activate();
	20
	21    orb->run();
	22    orb->destroy();
	23    return 0;
	24  }
> server-side: eg2_impl.cc
> client-side: eg2_clt.cc

# different address spaces : naming service

> initial contact with the Naming Service established via the root context
CORBA::ORB_ptr orb = CORBA::ORB_init(argc,argv);

CORBA::Object_var initServ;
initServ = orb->resolve_initial_references("NameService");

CosNaming::NamingContext_var rootContext;
rootContext = CosNaming::NamingContext::_narrow(initServ);

> server-side: eg3_impl.cc
> client-side: eg3_clt.cc


