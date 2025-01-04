
#1.Image (Uygulamayý publish eden image)
FROM mcr.microsoft.com/dotnet/sdk:8.0 as build
WORKDIR /app
#Build aþamasýnda sadece csproj dosyalarýný alýyoruz ve restore iþlemi yapýyoruz
#Bu iþlemi yapmamýzýn sebebi herhangi bir dosya deðiþtiðinde sadece o dosyanýn build iþlemi yapýlmasýný saðlamak
COPY *.csproj .
RUN dotnet restore 
COPY . . 
RUN dotnet publish AspNetCoreMvc.csproj -c Release -o out 

#2. Image (Uygulamayý çalýþtýran image)
#publish iþleminden sonra daha düþük boyutlu olan runtime imagemizi alýyoruz
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
#Copy iþlemi yapýlýrken build aþamasýnda oluþturulan out klasöründeki dosyalarý alýyoruz ve /app klasörüne kopyalýyoruz
COPY --from=build /app/out . 
ENV ASPNETCORE_URLS="http://*:4500" 
ENTRYPOINT ["dotnet", "AspNetCoreMvc.dll"]

