# Flex ColdFusion Integration- Web Project

This is an introduction to integrate flex and coldfusion with simple steps.

Create a cfc file that exposes methods to flex with acess set to remote under wwwroot directory as below

Folder Path:
D:\ColdFusion11\cfusion\wwwroot\FlexColdFusionWeb

my_service.cfc

```cfc
<cfcomponent>
	<cffunction name="sayHello" access="remote">		
		<cfreturn 'hello from coldfusion'>
	</cffunction>
</cfcomponent>

```

# Flex Server Settings

Create a new flex project with "FlexColdFusionWeb" project name. 

Selecct "ColdFusion" under Application service type dropdown list. 

Add below details for flex server settings

Colfusion Root Folder: D:\ColdFusion11\cfusion
Web root: D:\ColdFusion11\cfusion\wwwroot
Root URL: http://localhost:8500
Output folder: D:\ColdFusion11\cfusion\wwwroot\FlexColdFusionWeb

Flex will call "sayHello" method of "my_service" coldfuion component through flex remoting. 

```mxml
<s:RemoteObject id="service"
						source="FlexColdFusionWeb.my_service"
						destination="ColdFusion"
						result="service_resultHandler(event)"
						fault="service_faultHandler(event)"/>

```

Path: "D:\ColdFusion11\cfusion\wwwroot\FlexColdFusionWeb\my_service.cfc"

Source: "FlexColdFusionWeb.my_service"

Here is complete flex code that make calls to coldfusion service and shows the result recieved.

FlexColdFusionWeb.mxml 
```mxml
<?xml version="1.0" encoding="utf-8"?>
<s:Application xmlns:fx="http://ns.adobe.com/mxml/2009"
			   xmlns:s="library://ns.adobe.com/flex/spark"
			   xmlns:mx="library://ns.adobe.com/flex/mx"
			   minWidth="955"
			   minHeight="600"
			   creationComplete="application1_creationCompleteHandler(event)">
	<fx:Script>
		<![CDATA[
			import mx.controls.Alert;
			import mx.events.FlexEvent;
			import mx.rpc.events.FaultEvent;
			import mx.rpc.events.ResultEvent;
			import mx.utils.ObjectUtil;

			protected function service_resultHandler(event:ResultEvent):void
			{
				Alert.show(event.result.toString(), 'Result Recieved');
			}

			protected function service_faultHandler(event:FaultEvent):void
			{
				Alert.show(ObjectUtil.toString(event.fault), "Error");
			}

			protected function application1_creationCompleteHandler(event:FlexEvent):void
			{
				service.sayHello.send();
			}
		]]>
	</fx:Script>
	<fx:Declarations>
		<s:RemoteObject id="service"
						source="FlexColdFusionWeb.my_service"
						destination="ColdFusion"
						result="service_resultHandler(event)"
						fault="service_faultHandler(event)"/>
	</fx:Declarations>
</s:Application>
```


