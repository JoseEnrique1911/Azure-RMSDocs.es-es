# <a name="class-mippolicydescriptor"></a>clase mip::PolicyDescriptor 
Representa una directiva ad-hoc asociada al contenido protegido.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetName()  |  Obtiene el nombre de directiva.
 public void SetName(const std::string& value)  |  Establece el nombre de la directiva.
 public const std::string& GetDescription()  |  Obtiene la descripción de la directiva.
 public void SetDescription(const std::string& value)  |  Establece la descripción de la directiva.
public const std::vector<UserRights>& GetUserRightsList() const  |  Obtiene una colección de asignaciones de usuarios a derechos.
public const std::vector<mip::UserRoles>& GetUserRolesList()  |  Obtiene una colección de asignaciones de usuarios a roles
public const std::chrono::time_point<std::chrono::system_clock>& GetContentValidUntil()  |  Obtiene la hora de expiración de la directiva.
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  Establece la hora de expiración de la directiva.
 public bool DoesAllowOfflineAccess()  |  Determina si la directiva permite o no el acceso a contenido sin conexión.
 public void SetAllowOfflineAccess(bool value)  |  Establece si la directiva permite o no el acceso a contenido sin conexión.
 public const std::string& GetReferrer() const  |  Obtiene la dirección del sitio de referencia de directiva.
 public void SetReferrer(const std::string& uri)  |  Establece la dirección del sitio de referencia de directiva.
 public const AppDataHashMap& GetEncryptedAppData()  |  Obtiene datos específicos de la aplicación que se cifraron.
 public void SetEncryptedAppData(const AppDataHashMap& value)  |  Establece los datos específicos de la aplicación que fueron cifrados.
 public const AppDataHashMap& GetSignedAppData()  |  Obtiene datos específicos de la aplicación que se firmaron.
 public void SetSignedAppData(const AppDataHashMap& value)  |  Establece los datos específicos de la aplicación que deben firmarse.
  
## <a name="members"></a>Miembros
  
### <a name="getname"></a>GetName
Obtiene el nombre de directiva.

  
**Devuelve**: nombre de la directiva
  
### <a name="setname"></a>SetName
Establece el nombre de la directiva.

Parámetros:  
* **value**: nombre de la directiva


  
### <a name="getdescription"></a>GetDescription
Obtiene la descripción de la directiva.

  
**Devuelve**: descripción de la directiva
  
### <a name="setdescription"></a>SetDescription
Establece la descripción de la directiva.

Parámetros:  
* **value**: descripción de la directiva


  
### <a name="userrights"></a>UserRights
Obtiene una colección de asignaciones de usuarios a derechos.

  
**Devuelve**: colección de asignaciones de usuarios a derechos. El valor de la propiedad UserRightsList estará vacía si el usuario actual no tiene acceso a la información de derechos del usuario (es decir, no es el propietario y no tiene el derecho VIEWRIGHTSDATA).
  
### <a name="mipuserroles"></a>mip::UserRoles
Obtiene una colección de asignaciones de usuarios a roles

  
**Devuelve**: colección de asignaciones de usuarios a roles
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
Obtiene la hora de expiración de la directiva.

  
**Devuelve**: hora de expiración de la directiva
  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
Establece la hora de expiración de la directiva.

Parámetros:  
* **value**: hora de expiración de la directiva


  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
Determina si la directiva permite o no el acceso a contenido sin conexión.

  
**Devuelve**: si la directiva permite o no el acceso a contenido sin conexión (valor predeterminado = true)
  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
Establece si la directiva permite o no el acceso a contenido sin conexión.

Parámetros:  
* **value**: si la directiva permite o no el acceso a contenido sin conexión


  
### <a name="getreferrer"></a>GetReferrer
Obtiene la dirección del sitio de referencia de directiva.

  
**Devuelve**: dirección del sitio de referencia de la directiva. El sitio de referencia es una URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para tener acceso al contenido.
  
### <a name="setreferrer"></a>SetReferrer
Establece la dirección del sitio de referencia de directiva.

Parámetros:  
* **uri**: dirección del sitio de referencia de directiva


El sitio de referencia es una URI que puede mostrarse al usuario cuando la adquisición de la directiva ha producido un error y que contiene información sobre cómo el usuario puede obtener permiso para tener acceso al contenido.
  
### <a name="appdatahashmap"></a>AppDataHashMap
Obtiene datos específicos de la aplicación que se cifraron.

  
**Devuelve**: datos específicos de la aplicación. Una clase [UserPolicy](class_mip_userpolicy.md) puede contener un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos cifrados son independientes de los datos firmados accesibles mediante [PolicyDescriptor::GetSignedAppData](class_mip_policydescriptor.md#getsignedappdata)
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
Establece los datos específicos de la aplicación que fueron cifrados.

Parámetros:  
* **value**: datos específicos de la aplicación


Una aplicación puede especificar un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos cifrados son independientes del conjunto de datos firmado por [PolicyDescriptor::SetSignedAppData](class_mip_policydescriptor.md#setsignedappdata).
  
### <a name="appdatahashmap"></a>AppDataHashMap
Obtiene datos específicos de la aplicación que se firmaron.

  
**Devuelve**: datos específicos de la aplicación. Una clase [UserPolicy](class_mip_userpolicy.md) puede contener un diccionario de datos específicos de la aplicación firmados por el servicio RMS. Estos datos firmados son independientes de los datos cifrados accesibles mediante [PolicyDescriptor::GetEncryptedAppData](class_mip_policydescriptor.md#getencryptedappdata)
  
### <a name="setsignedappdata"></a>SetSignedAppData
Establece los datos específicos de la aplicación que deben firmarse.

Parámetros:  
* **value**: datos específicos de la aplicación


Una aplicación puede especificar un diccionario de datos específicos de la aplicación cifrados por el servicio RMS. Estos datos firmados son independientes del conjunto de datos cifrados por [PolicyDescriptor::SetEncryptedAppData](class_mip_policydescriptor.md#setencryptedappdata).