FROM mcr.microsoft.com/dotnet/aspnet:8.0 as BASE
WORKDIR /app
USER ${APP_UID}
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 as BUILD
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY "Dotnet.Homeworks.MainProject/Dotnet.Homeworks.MainProject.csproj" "Dotnet.Homeworks.MainProject/"
RUN dotnet restore "Dotnet.Homeworks.MainProject/Dotnet.Homeworks.MainProject.csproj"
COPY . .
WORKDIR "/src/Dotnet.Homeworks.MainProject"
RUN dotnet build -c $BUILD_CONFIGURATION -o ./build

FROM BUILD as PUBLISH
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish -c $BUILD_CONFIGURATION -o /app/publish -p:UseAppHost=false

FROM BASE as FINAL
COPY --from=PUBLISH /app/publish .
ENTRYPOINT ["dotnet", "publish/Dotnet.Homeworks.MainProject.dll"]