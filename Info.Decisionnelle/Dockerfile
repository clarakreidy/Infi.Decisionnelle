FROM mcr.microsoft.com/dotnet/core/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Info.Decisionnelle/Info.Decisionnelle.csproj", "Info.Decisionnelle/"]
RUN dotnet restore "Info.Decisionnelle/Info.Decisionnelle.csproj"
COPY . .
WORKDIR "/src/Info.Decisionnelle"
RUN dotnet build "Info.Decisionnelle.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Info.Decisionnelle.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Info.Decisionnelle.dll"]
