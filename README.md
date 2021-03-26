# Reverse proxy
* https://boersenclient.moonstonks.space -> Boersenclient (16000)
* https://privat.moonstonks.space -> Privatkundenbrokerfrontend (16010)
* https://business.moonstonks.space -> Geschäftskundenbrokerfrontend (16020)
* https://simulation.moonstonks.space -> Simulationsfrontend (16030)

# Docker Container
## Ports:
* SSH: 16022
* Wertpapiermarkt - Frontend: 16000
* Wertpapiermarkt - Backend: 16001
* Privatkundenbroker - Frontend: 16010
* Privatkundenbroker - Backend: 16011
* Geschäftskundenbroker - Frontend: 16020
* Geschäftskundenbroker - Backend: 16021
* Simulation - Frontend: 16030
* Simulation - Backend: 16031

# CI/CD Pipeline

Mithilfe von Github Actions wird ein Workflow definiert, der bei einem Release den Dockercontainer eines Repositories baut und nach Dockerhub pusht. Im Anschluss wird auf dem Server ein neues Deployment des Image getriggert.
Dies kann auf zwei Arten erledigt, werden die noch evaluiert werden müssen:

1. Hinterlegen eines Webhooks auf Dockerhub, sodass bei jedem neu gepushten Image der Server die Möglichkeit hat dieses zu pullen und bereitzustellen
2. Direkter Call eines Endpunkts/Direct Acces via SSH auf den Sever, der das neu gepushte Image bereitstellt.
3. **Einfachste Möglichkeit** Nutzung von [Watchtower](https://containrrr.dev/watchtower/). Watchtower sorgt automatisch dafür, dass nach einem bestimmten Zeitintervall überprüft wird, ob ein neues Image auf Dockerhub vorhanden ist. Im Anschluss wird das Image automatisch gepullt und mit gleicher Konfiguration wie das vorherige bereitgestellt.
