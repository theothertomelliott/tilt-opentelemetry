# Tilt Telemetry

A [Tilt Extension](https://docs.tilt.dev/extensions.html) for working with [Opentelemetry](https://opentelemetry.io/).
It provides a pre-configured opentelemetry collector and an instance of [Jaeger](https://www.jaegertracing.io/) to gather, store and view traces.
You can run the provided resources either in Kubernetes or Docker Compose.

# Usage

To import this repo for use, add the following to your `Tiltfile`:

```
v1alpha1.extension_repo(name='tilt-opentelemetry', url='http://github.com/theothertomelliott/tilt-opentelemetry')
v1alpha1.extension(name='tilt-opentelemetry', repo_name='tilt-opentelemetry', repo_path='')
```

Then you can import the appropriate functions either for Kubernetes or Docker Compose.

## Kubernetes

```
load('ext://tilt-opentelemetry', 'opentelemetry_kubernetes')
opentelemetry_kubernetes()
```

## Docker Compose

```
load('ext://tilt-opentelemetry', 'opentelemetry_compose')
opentelemetry_compose()
```