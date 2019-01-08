FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["WXServiceCore/WXServiceCore.csproj", "WXServiceCore/"]
RUN dotnet restore "WXServiceCore/WXServiceCore.csproj"
COPY . .
WORKDIR "/src/WXServiceCore"
RUN dotnet build "WXServiceCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WXServiceCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WXServiceCore.dll"]