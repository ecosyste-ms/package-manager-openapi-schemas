# Package Manager OpenAPI Schemas

OpenAPI 3.0 specifications for many package manager registry APIs.

Initially extract from [packages.ecosyste.ms](https://github.com/ecosyste-ms/packages) and existing openapi specs.

## Available Schemas

| Ecosystem | Registry | Schema | Official Spec |
|-----------|----------|--------|---------------|
| **NPM** | registry.npmjs.org | [`npm.yaml`](openapi/npm.yaml) | - |
| **Go** | proxy.golang.org | [`go.yaml`](openapi/go.yaml) | - |
| **NuGet** | nuget.org | [`nuget.yaml`](openapi/nuget.yaml) | - |
| **PyPI** | pypi.org | [`pypi.yaml`](openapi/pypi.yaml) | - |
| **Maven** | repo1.maven.org | [`maven.yaml`](openapi/maven.yaml) | - |
| **Packagist** | packagist.org | [`packagist.yaml`](openapi/packagist.yaml) | - |
| **Cargo** | crates.io | [`cargo.json`](openapi/cargo.json) | [OpenAPI 3.1.0](https://crates.io/api/openapi.json) |
| **RubyGems** | rubygems.org | [`rubygems.yaml`](openapi/rubygems.yaml) | - |
| **Pub** | pub.dev | [`pub.yaml`](openapi/pub.yaml) | - |
| **Hex** | hex.pm | [`hex.yaml`](openapi/hex.yaml) | - |
| **OpenVSX** | open-vsx.org | [`openvsx.json`](openapi/openvsx.json) | [OpenAPI 3.1.0](https://open-vsx.org/v3/api-docs/registry) |
| **Deno** | apiland.deno.dev | [`deno.yaml`](openapi/deno.yaml) | - |
| **Homebrew** | formulae.brew.sh | [`homebrew.yaml`](openapi/homebrew.yaml) | - |
| **CPAN** | metacpan.org | [`cpan.yaml`](openapi/cpan.yaml) | - |
| **Conda** | anaconda.org | [`conda.yaml`](openapi/conda.yaml) | - |
| **Docker** | hub.docker.com | [`docker.yaml`](openapi/docker.yaml) | - |
| **Puppet** | forgeapi.puppet.com | [`puppet.yaml`](openapi/puppet.yaml) | - |
| **Elm** | package.elm-lang.org | [`elm.yaml`](openapi/elm.yaml) | - |
| **Cocoapods** | cocoapods.org | [`cocoapods.yaml`](openapi/cocoapods.yaml) | - |
| **Clojars** | clojars.org | [`clojars.yaml`](openapi/clojars.yaml) | - |
| **Terraform** | registry.terraform.io | [`terraform.yaml`](openapi/terraform.yaml) | - |
| **ArtifactHub** | artifacthub.io | [`artifacthub.yaml`](openapi/artifacthub.yaml) | - |
| **WordPress** | api.wordpress.org | [`wordpress.yaml`](openapi/wordpress.yaml) | - |
| **Drupal** | packages.drupal.org | [`drupal.yaml`](openapi/drupal.yaml) | - |

## Usage

### Generate API Clients

```bash
openapi-generator-cli generate -i openapi/npm.yaml -g python -o npm-client
openapi-generator-cli generate -i openapi/cargo.json -g typescript-axios -o cargo-client
# 50+ languages supported
```

### Interactive Documentation

```bash
docker run -p 8080:8080 -e SWAGGER_JSON=/schemas/openapi/npm.yaml -v $(pwd):/schemas swaggerapi/swagger-ui
```

### Mock Servers

```bash
npm install -g @stoplight/prism-cli
prism mock openapi/npm.yaml
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

**Quick start:**
1. Copy an existing schema as template
2. Document the API endpoints
3. Validate: `swagger-cli validate openapi/your_ecosystem.yaml`
4. Update this README
5. Submit PR

## License

MIT License - see [LICENSE](LICENSE) for details.

Note: Schemas sourced from official specifications (marked in the table above) retain their original licenses as defined in the respective spec files.
