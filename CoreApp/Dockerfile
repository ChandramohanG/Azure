#FROM microsoft/aspnetcore:2.0 
#ARG source
#WORKDIR /app
#EXPOSE 80
#COPY ${source:-obj/Docker/publish} .
#ENTRYPOINT ["dotnet", "CoreApp.dll"]
FROM microsoft/iis
	ARG source
	WORKDIR /app
	EXPOSE 8081

	RUN ["powershell.exe", "Install-WindowsFeature NET-Framework-45-ASPNET"]  
	RUN ["powershell.exe", "Install-WindowsFeature Web-Asp-Net45"]

	RUN powershell New-Website -Name 'my-app' -Port 8081 -PhysicalPath 'c:\app' -ApplicationPool '.NET v4.5'
	
	#RUN powershell -NoProfile -Command \
	    #Import-module IISAdministration; \
	    #New-IISSite -Name "Site" -PhysicalPath "C:\app" -BindingInformation "*:80:"; \
		#Enable-WindowsOptionalFeature -Online -FeatureName "IIS-ApplicationDevelopment"; \
		#Enable-WindowsOptionalFeature -Online -FeatureName "IIS-WindowsAuthentication"; \
		#Enable-WindowsOptionalFeature -Online -FeatureName "IIS-URLAuthorization" 
	
	COPY ${source:-obj/Docker/publish} .
	ENTRYPOINT ["dotnet", "CoreApp.dll"]