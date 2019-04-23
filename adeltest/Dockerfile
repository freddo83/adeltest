FROM mcr.microsoft.com/dotnet/core/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS build
WORKDIR /src
COPY ["adeltest/adeltest.csproj", "adeltest/"]

RUN dotnet restore "adeltest/adeltest.csproj"
COPY . .
WORKDIR "/src/adeltest"
RUN dotnet build "adeltest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "adeltest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "adeltest.dll"]