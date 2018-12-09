FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 50651
EXPOSE 44362

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["ArtifactApprove/ArtifactApprove.csproj", "ArtifactApprove/"]
RUN dotnet restore "ArtifactApprove/ArtifactApprove.csproj"
COPY . .
WORKDIR "/src/ArtifactApprove"
RUN dotnet build "ArtifactApprove.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ArtifactApprove.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ArtifactApprove.dll"]