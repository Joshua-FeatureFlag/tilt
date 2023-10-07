load("ext://helm_remote", "helm_remote")

analytics_settings(enable=False)
update_settings(max_parallel_updates=2)

arch = (
    str(
        local(
            "uname -m",
            command_bat="echo %PROCESSOR_ARCHITECTURE%",
            quiet=True,
            echo_off=True,
        )
    )
    .rstrip()
    .lower()
)
is_arm = arch == "arm64"


# Infrastructure
# helm_remote(
#     "localstack",
#     repo_name="localstack-charts",
#     repo_url="https://localstack.github.io/helm-charts",
#     set=[
#         "livenessProbe.initialDelaySeconds=60",
#         "readinessProbe.initialDelaySeconds=60",
#     ],
# )
# k8s_resource("localstack", port_forwards="4566:4566", labels=["infrastructure"])

helm_remote(
    "postgresql",
    repo_name="bitnami",
    repo_url="https://charts.bitnami.com/bitnami",
    set=[
        "global.postgresql.auth.postgresPassword=password",
        "global.postgresql.auth.username=featureflag",
        "global.postgresql.auth.password=password",
        "global.postgresql.auth.database=featureflag_dev",
        "primary.extendedConfiguration=password_encryption = md5",
    ],
)
k8s_resource("postgresql", port_forwards="5432:5432", labels=["infrastructure"])

services = [
    "frontend",
]

for service in services:
    if os.path.exists("../" + service):
        include("../" + service + "/Tiltfile")
    else:
        warn("Cannot find " + service + " repo. Service will not be available.")