
#1.Image (Uygulamay� publish eden image)
FROM mcr.microsoft.com/dotnet/sdk:8.0 as build
WORKDIR /app
#Build a�amas�nda sadece csproj dosyalar�n� al�yoruz ve restore i�lemi yap�yoruz
#Bu i�lemi yapmam�z�n sebebi herhangi bir dosya de�i�ti�inde sadece o dosyan�n build i�lemi yap�lmas�n� sa�lamak
COPY *.csproj .
RUN dotnet restore 
COPY . . 
RUN dotnet publish AspNetCoreMvc.csproj -c Release -o out 

#2. Image (Uygulamay� �al��t�ran image)
#publish i�leminden sonra daha d���k boyutlu olan runtime imagemizi al�yoruz
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
#Copy i�lemi yap�l�rken build a�amas�nda olu�turulan out klas�r�ndeki dosyalar� al�yoruz ve /app klas�r�ne kopyal�yoruz
COPY --from=build /app/out . 
ENV ASPNETCORE_URLS="http://*:4500" 
ENTRYPOINT ["dotnet", "AspNetCoreMvc.dll"]

