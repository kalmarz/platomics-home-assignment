# README #

## Notes ##

### Kubernetes workload challenge ###

- Point 5: "Confirm the functionality of the ReadinessProbe"
  - The backend app wouldn't start without a working probe therefore a running pod automatically confirms the probe's functionality.
- Point 6: "Confirm the functionality of the newly created NetworkPolicy"
  - To confirm it, the cluster has to have a network policy engine running, like Calico, Amazon VPC CNI with network policies enabled, etc.
  - Exec into the backed pod and run the following commands:
    - `wget -T5 -O- http://db1.project-plato.svc.cluster.local:6379` -> should answer
    - `wget -T5 -O- http://db2.project-plato.svc.cluster.local:5432` -> should answer
    - `wget -T5 -O- http://httpforever.com/` -> should give a timeout
- Point 7: "Confirm the availability of the Secret contents in the Deployment"
  - Exec into the db2 pod and run the following command: `env | grep ADMIN`
- Bonus: Postgres
  - The manifest assumes FluxCD running on the cluster and picking up the changes from the Git repository and reconciling them.
  - The `HelmRelease` manifest runs with the default values, it only enables the Prometheus exporter as an extra.
- Bonus: kube-prometheus-stack
  - The manifest assumes FluxCD running on the cluster and picking up the changes from the Git repository and reconciling them.
  - The `HelmRelease` manifest runs with the default values, it only adds a scrape config for Postgres.
