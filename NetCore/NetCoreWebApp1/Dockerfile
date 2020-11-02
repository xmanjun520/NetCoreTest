FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["NetCoreWebApp1/NetCoreWebApp1.csproj", "NetCoreWebApp1/"]
RUN dotnet restore "NetCoreWebApp1/NetCoreWebApp1.csproj"
COPY . .
WORKDIR "/src/NetCoreWebApp1"
RUN dotnet build "NetCoreWebApp1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreWebApp1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreWebApp1.dll"]