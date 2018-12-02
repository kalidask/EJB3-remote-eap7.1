# EJB3-remote-eap7.1


EJB3 Client side Chnages:
-----------------------------------------------
Initialize the context in following way:

InitialContext context = new WildFlyInitialContext();

add import "org.wildfly.naming.client.WildFlyInitialContext" to your JSP/servlet

EJB lookup should be in following form:

e.g :

String myURl="/Calculator_EJB3/CalculatorBean!com.javacodegeeks.ejb.CalculatorRemote";
 ops = (CalculatorRemote)  context.lookup("ejb:"+myURl);

Add "wildfly-config.xml" into your application META-INF directory

<configuration>
  <jboss-ejb-client xmlns="urn:jboss:wildfly-client-ejb:3.0">
    <connections>
      <connection uri="remote+http://REMOTE-SERVER-IP:8080"/>
    </connections>
  </jboss-ejb-client>
  <authentication-client xmlns="urn:elytron:1.0">
    <authentication-rules>
      <rule use-configuration="ejb"/>
    </authentication-rules>
    <authentication-configurations>
      <configuration name="ejb">
        <set-user-name name="admin"/>
        <credentials>
          <clear-password password="admin"/>
        </credentials>
      </configuration>
    </authentication-configurations>
  </authentication-client>
</configuration>


EJB3 Server side changes:

-----------------------------------------------
Add application user:

$JBOSS_HOME/bin:  ./add-user.sh -a -u admin -p admin

Note: make sure have applied jboss eap 7.1.3 patch to eap.
