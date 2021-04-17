#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY aspnetcore5-with-nextjs/aspnetcore5-with-nextjs.csproj aspnetcore5-with-nextjs/
RUN dotnet restore "aspnetcore5-with-nextjs/aspnetcore5-with-nextjs.csproj"
COPY . .
WORKDIR "/src/aspnetcore5-with-nextjs"
RUN dotnet build "aspnetcore5-with-nextjs.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcore5-with-nextjs.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcore5-with-nextjs.dll"]
