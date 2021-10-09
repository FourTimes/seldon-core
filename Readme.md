Seldon - an open source platform to deploy your machine learning models on Kubernetes at massive scale.


![Architeture](images/seldon-core-high-level.jpg)


Concept:

<code>
<i><b>Seldon</b>core converts your ML models into production ready REST/gRPC microservices.</i>
<br>
<br>
</code>


These are Seldon Core main components:

    1. Reusable and non-reusable model servers
    2. Language Wrappers to containerise models
    3. SeldonDeployment CRD and Seldon Core Operator
    4. Service Orchestrator for advanced inference graphs

as well as integration with third-party systems

    1. Kubernetes Ingress integration with Ambassador and Istio
    2. Metrics with Prometheus
    3. Tracing with Jaeger
    4. Endpoint Documentation with OpenApi (swagger)
