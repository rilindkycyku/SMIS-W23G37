FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["W23G37.csproj", "./"]
RUN dotnet restore "./W23G37.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "W23G37.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "W23G37.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "W23G37.dll"]
