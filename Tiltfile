def setup_telemetry(
    local=False,
    namespace="default",
    labels=["telemetry"]
    ):
    tfdir = os.path.dirname(__file__)
    if local:
        setup_local(tfdir, labels)
    else:
        setup_kubernetes(namespace,labels)

def setup_local(tfdir, labels):
    docker_compose(os.path.join(tfdir, 'compose/docker-compose.yaml'),)
    # local_resource(
    #     "jaeger",
    #     serve_cmd="""docker run --rm \
    #         --platform=linux/amd64 \
    #         -e COLLECTOR_ZIPKIN_HTTP_PORT=9411 \
    #         -p 5775:5775/udp \
    #         -p 6831:6831/udp \
    #         -p 6832:6832/udp \
    #         -p 5778:5778 \
    #         -p 16686:16686 \
    #         -p 14268:14268 \
    #         -p 9411:9411 \
    #         jaegertracing/all-in-one:1.6""",
    #     labels=labels,
    #     links=[link("http://localhost:16686", "Jaeger UI")]
    # )

def setup_kubernetes(tfdir, namespace, labels):
    # Load the Tilt support Helm chart
    k8s_yaml(helm(
        os.path.join(tfdir, 'charts/otel'),
        namespace=namespace,
    ))
    k8s_resource(
        "jaeger", 
        port_forwards="16686:16686",
        labels=labels
    )
    k8s_resource(
        "otel-agent",
        labels=labels
    )
    k8s_resource(
        "otel-collector",
        labels=labels
    )