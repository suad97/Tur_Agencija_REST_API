FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /TurAgencijaRS2_WebApi

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /TurAgencijaRS2_WebApi
COPY --from=build-env TurAgencijaRS2_WebApi/out .

CMD dotnet TurAgencijaRS2_WebApi.dll --urls "http://*:$PORT"