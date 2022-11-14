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
    docker_compose(os.path.join(tfdir, 'compose/docker-compose.yaml'))
    dc_resource('jaeger', labels=labels)
    dc_resource('otel-collector', labels=labels)

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