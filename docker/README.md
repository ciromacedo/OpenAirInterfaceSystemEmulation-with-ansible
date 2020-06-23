# Build Docker Image
The build process is executed as of **Ubuntu 18.04**. 

To perform this step, do the following:
1. Build Open5GSLte image ``` docker build -f open5GSLte.dockerFile -t laboraufg/epc-open5gs . ```
2. Build Web User Interface of Open5GSLte ``` docker build -f webuiOpen5GSLte.dockerFile -t laboraufg/webui-open5gs . ```
<!-- 2. Build free5gc-stage-1 image ```docker build -f free5gc.dockerFile -t laboraufg/free5gc-st1 . ```
3. Build web user interface of free5gc-stage-1 image ``` docker build -f webui.dockerFile -t laboraufg/webui-free5gc .```
4. Build Evolved Node B **(enB)** of OpenAirSim image ``` docker build -f enb.dockerFile -t laboraufg/enb-openairsim .```
5. Build User Equipment **(ue)** of OpenAirSim image ``` docker build -f ue.dockerFile -t laboraufg/ue-openairsim .```
-->

After build finish, the next step is publish in [Docker Hub](https://hub.docker.com/u/laboraufg) (to publish you need is member of laboraufg team in [Docker Hub](https://hub.docker.com/u/laboraufg)). To publish you need login in your docker account. Into a terminal, type ```docker login``` then inform your docker ```user / password```. After connecting, publish the images generated in the previous step with the following commands:
```
docker push laboraufg/epc-open5gs
docker push laboraufg/webui-open5gs
```