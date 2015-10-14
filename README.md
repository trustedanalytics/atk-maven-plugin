
Atk Maven Plugin
================

Includes Mojo for generating atk-module-generated.conf file at build time

#Building
Before building/deploying you will add the trustedanalytics.org certificate to your java key store
```
openssl s_client -connect maven.trustedanalytics.org:443 -showcerts < /dev/null | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > `pwd`/public.crt &&\
sudo keytool -importcert -trustcacerts -storepass changeit -file `pwd`/public.crt \
-alias trustedanalytics.org  \
-keystore `find $JAVA_HOME -name cacerts`
```
If opensssl times out you can try
```
wget https://s3-us-west-2.amazonaws.com/analytics-tool-kit/public.crt -O `pwd`/public.crt &&\
sudo keytool -importcert -trustcacerts -storepass changeit -file `pwd`/public.crt \
-alias trustedanalytics.org  \
-keystore `find $JAVA_HOME -name cacerts`
```
```
...
Trust this certificate? [no]:  yes
Certificate was added to keystore
```
When prompted accept the key.


You can also bypass certificate verification all together
```
MAVEN_OPTS="-Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true"
```


Regardless of the option you choose the following will need to be added to **MAVEN_OPTS**

```
-Dhttps.protocols=TLSv1.2
```

