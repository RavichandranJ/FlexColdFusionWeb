# Flex ColdFusion Integration- Web Project

This is an introduction to integrate flex and coldfusion with simple steps.

Create a cfc file that exposes methods to flex with acess set to remote under wwwroot directory as below

Folder Path:
D:\ColdFusion11\cfusion\wwwroot\FlexColdFusionWeb

my_service.cfc
<cfcomponent>
	<cffunction name="sayHello" access="remote">		
		<cfreturn 'hello from coldfusion'>
	</cffunction>
</cfcomponent>




