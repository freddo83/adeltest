FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
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