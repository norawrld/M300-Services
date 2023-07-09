Dockerfile:

FROM google/cadvisor:latest

# Exponieren des cAdvisor-Ports
EXPOSE 8080

# Starten von cAdvisor
CMD ["/usr/bin/cadvisor", "--logtostderr", "--port=8080"]

Image erstellen:
![Screenshot 2023-07-10 000727](https://github.com/norawrld/M300-Services/assets/87812697/b661a531-571e-4dc5-97d6-d96f05dbfeaa)

Container erstellen:
![Screenshot 2023-07-10 000806](https://github.com/norawrld/M300-Services/assets/87812697/8828b815-fb39-4995-b634-1ed549164da0)


![Screenshot 2023-07-10 000837](https://github.com/norawrld/M300-Services/assets/87812697/7f4f8996-3a42-422f-92c5-2d64c63c649d)

