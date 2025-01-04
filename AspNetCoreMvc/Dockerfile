#Seçtiðimiz image içerisind .Net CLI barýndýrmasý gerektiðinden .Net Core SDK image'ýný kullanýyoruz.
FROM mcr.microsoft.com/dotnet/sdk:8.0
WORKDIR /app
#Ýlk nokta dockerfile'ýn bulunduðu dizini temsil eder. Ýkinci nokta ise image içerisindeki çalýþma dizinini temsil eder.
COPY . . 
#publish iþlemi öncesinde projenin baðýmlýlýklarýný restore ediyoruz.
RUN dotnet restore AspNetCoreMvc.csproj 
#AspNetCoreMvc.csprojemizi release modunda out klasörüne publish ediyoruz.
RUN dotnet publish AspNetCoreMvc.csproj -c Release -o out 
#Çalýþma dizinimizi out klasörü olarak belirliyoruz.
WORKDIR out 
#Uygulamamýz ayaða kalktýðýnda default olarak localhost:5000 adresinde çalýþacaktýr.Bu yüzden dýþarýdan eriþim saðlayabilmek için port 4500'i environment olarak belirttik.
#Uygulamamýzýn hangi portta çalýþacaðýný belirtiyoruz.
ENV ASPNETCORE_URLS="http://*:4500" 
ENTRYPOINT ["dotnet", "AspNetCoreMvc.dll"]

