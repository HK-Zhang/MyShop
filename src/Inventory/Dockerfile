FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 5000

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Inventory/Inventory.csproj", "Inventory/"]
RUN dotnet restore "Inventory/Inventory.csproj"
COPY . .
WORKDIR "/src/Inventory"
RUN dotnet build "Inventory.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Inventory.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Inventory.dll"]