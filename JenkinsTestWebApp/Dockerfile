FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["JenkinsTestWebApp/JenkinsTestWebApp.csproj", "JenkinsTestWebApp/"]
RUN dotnet restore "JenkinsTestWebApp/JenkinsTestWebApp.csproj"
COPY . .
WORKDIR "/src/JenkinsTestWebApp"
RUN dotnet build "JenkinsTestWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "JenkinsTestWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "JenkinsTestWebApp.dll"]