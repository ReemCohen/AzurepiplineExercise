
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine AS base
WORKDIR /app
EXPOSE 5000 
ENV ASPNETCORE_URLS=http://+:5000
 
FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS build
WORKDIR /src
COPY .
RUN dotnet restore "AzurepiplineExercise/AzurepiplineExercise.csproj"
COPY . .
WORKDIR "/src/AzurepiplineExercise"
RUN dotnet build "AzurepiplineExercise.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AzurepiplineExercise.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AzurepiplineExercise.dll"]