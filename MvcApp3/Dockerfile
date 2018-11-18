FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 61152
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["/MvcApp3.csproj", "MvcApp3/"]
RUN dotnet restore "MvcApp3/MvcApp3.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "MvcApp3.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MvcApp3.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MvcApp3.dll"]