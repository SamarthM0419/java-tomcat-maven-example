# tomcat installation:

sudo apt update
sudo apt install -y openjdk-17-jdk

cd /opt
sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.105/bin/apache-tomcat-9.0.105.tar.gz
sudo tar -xvzf apache-tomcat-9.0.105.tar.gz
sudo mv apache-tomcat-9.0.105 tomcat9
sudo nano /opt/tomcat9/conf/server.xml

Find:

<Connector port="8080"

Change to:

<Connector port="8081"

sudo -i
cd /opt/tomcat9/bin
chmod +x *.sh
./startup.sh
ss -tulnp | grep 8081

To create a user in Apache Tomcat 9 for accessing Manager/Admin apps:

1. Open tomcat-users.xml
sudo subl /opt/tomcat9/conf/tomcat-users.xml
2. Add user and roles

Before the closing line:
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="admin-gui"/>

<user username="sriram"
      password="sriram123"
      roles="manager-gui,manager-script,admin-gui"/>
      
Allow remote access to Manager/Admin pages

Edit Manager context:

sudo subl /opt/tomcat9/webapps/manager/META-INF/context.xml

Comment/remove this section:

<Valve className="org.apache.catalina.valves.RemoteAddrValve"
       allow="127\.\d+\.\d+\.\d+|::1"/>

Do the same for Admin app:

sudo subl /opt/tomcat9/webapps/host-manager/META-INF/context.xml

sudo /opt/tomcat9/bin/shutdown.sh
sudo /opt/tomcat9/bin/startup.sh
http://<server-ip>:8081/manager/html


