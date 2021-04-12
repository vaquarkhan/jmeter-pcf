= Application Autoscaling

== Reading

Cloud Foundry has some services for auto scaling applications. These serve as a starting point and may work for some of your application portfolio. Read about them link:http://docs.pivotal.io/pivotalcf/autoscaling[on pivotal site].


Try following the directions above for your app.

A good start for load testing is jMeter. You can download that link:http://jmeter.apache.org/download_jmeter.cgi[here]. jMeter requires you have a JDK installed!

== Goal

In this section you will leverage Pivotal's Autoscaling Service to scale your microservice.

== Exercise

=== Configuring Autoscaling

. Using Apps Manager, create a new instance of the Autoscaler from the Marketplace.
+
* Be sure to name your service instance: <first-initial><last-initial>-cities-service-autoscaler
* Be sure to select the Gold plan
* Bind this instance to your cities-service

. Follow the instructions on link:http://docs.pivotal.io/pivotalcf/autoscaling[Autoscaling] to configure and enable your autoscaling service.

. Launch the autoscaling dashboard for your service.


=== Set memory to ensure scaling will happen

Be sure to set the memory allocation for your application to 650M to ensure the application will scale.


=== Generating Load and Observing Results

. link:http://jmeter.apache.org/download_jmeter.cgi[Apache JMeter] Can be used to generate load.

. Use the following link:https://raw.githubusercontent.com/krujos/pcf-workshop/master/dev-experience/cities-load-generator.jmx[JMeter script] as a starting point. Thanks link:https://github.com/gtantachuco-pivotal[Guillermo Tantachuco]!!!

. Open the 'cities-load-generator.jmx' in the JMeter GUI.

. Expand the content of the JMeter test plan by: i) selecting the 'Load Generator' test plan on the left pane; and, ii) going to the menu: 'Option -> Expand All'

. Edit the test plan to use your application's URL. To do so, change the 'Server Name or IP' field on the 'HTTP Request Defaults' item.

. Save the test plan: 'File -> Save'

. Run the test plan: 'Run -> Start'

. Use both the developer console and the auto-scale console to observe your service scale up and back down based on load. [Optional] See app metrics on the App Dynamics' console.

. Stop the test plan: 'Run -> Stop'

== Checking your work

. An autoscaling service instance should show correctly under the VCAP_SERVICES environment variable.
+
[source,bash]
----
$ cf env <first-inital><last-initial>-cities-service
----

. Your app should scale up when the jmeter script is executed and back down after the script completes.
