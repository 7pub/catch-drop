# Snapdrop Inspired by Apple's Airdrop 

[Snapdrop](https://showtime.one): Sende Bilder/Musik im eigenen Heimnetzwerk. Ganz ohne Installation
#### Snapdrop ist mit den folgenden Technologien aufgebaut:
* Vanilla HTML5 / ES6 / CSS3  
* Progressive Web App
* [WebRTC](http://webrtc.org/)
* [WebSockets](http://www.websocket.org/)
* [NodeJS](https://nodejs.org/en/)
* [Material Design](https://material.google.com/)

## Support the Snapdrop Community
Snadprop ist und bleibt kostenlos. 
Trotzdem müssen wir für den Server bezahlen.
Wer kann und die Zeit dazu hat, "Robin" würde sich sicher freuen. 

Wenn Sie beitragen möchten, verwenden Sie bitte PayPal:
[<img src="https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif">](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=74D2NE84JHCWG&source=url)

or Bitcoin:

[<img src="https://coins.github.io/thx/logo-color-large-pill-320px.png" alt="CoinThx" width="200"/>](https://coins.github.io/thx/#1K9zQ8f4iTyhKyHWmiDKt21cYX2QSDckWB?label=Snapdrop&message=Thanks!%20Your%20contribution%20helps%20to%20keep%20Snapdrop%20free%20for%20everybody!) 

Vielen Dank für die Unterstützung freier und offener Software!

##### Was ist mit der Verbindung? Handelt es sich um eine P2P-Verbindung direkt von Gerät zu Gerät oder gibt es einen Drittanbieter-Server?
Es verwendet eine P2P-Verbindung, wenn WebRTC vom Browser unterstützt wird. WebRTC benötigt einen Signaling Server, dieser dient aber nur dem Verbindungsaufbau und ist nicht an der Dateiübertragung beteiligt.

##### Was ist mit der Privatsphäre? Werden Dateien auf Drittanbieter-Servern gespeichert?
Keine Ihrer Dateien wird jemals an einen Server gesendet. Dateien werden nur zwischen Peers gesendet. Snapdrop verwendet nicht einmal eine Datenbank. Wenn Sie neugierig sind, schauen Sie sich [den Server] an (https://github.com/RobinLinus/snapdrop/blob/master/server/). Selbst wenn Snapdrop die übertragenen Dateien anzeigen könnte, verschlüsselt WebRTC die Dateien während der Übertragung, sodass der Server sie nicht lesen kann.

##### Was ist mit der Sicherheit? Werden meine Dateien verschlüsselt, während sie zwischen den Computern gesendet werden?
Ja. Ihre Dateien werden mit WebRTC gesendet, das sie während der Übertragung verschlüsselt.

##### Warum implementieren Sie Feature xyz nicht?
Snapdrop ist eine Studie in radikaler Einfachheit. Die Benutzeroberfläche ist wahnsinnig einfach. Features werden sehr sorgfältig ausgewählt, da die Komplexität quadratisch wächst, da jedes Feature potentiell mit jedem anderen Feature interferiert. Wir konzentrieren uns sehr eng auf einen einzigen Anwendungsfall: sofortige Dateiübertragung.
Wir versuchen nicht, für einige Grenzfälle zu optimieren. Wir optimieren den Benutzerfluss der durchschnittlichen Benutzer. Seien Sie nicht traurig, wenn wir Ihren Funktionswunsch der Einfachheit halber ablehnen.

## Local Development
[Install docker with docker-compose.](https://docs.docker.com/compose/install/)

Clone the repository:
```
    git clone https://github.com/RobinLinus/snapdrop.git
    cd snapdrop
    docker-compose up -d
```

To restart the containers run `docker-compose restart`.
To stop the containers run `docker-compose stop`.

Now point your browser to `http://localhost:8080`.
### Testen von PWA-bezogenen Funktionen
PWAs erfordern, dass die App unter einem korrekt eingerichteten und vertrauenswürdigen TLS-Endpunkt bereitgestellt wird.

Der nginx-Container erstellt für Sie ein CA-Zertifikat und ein Website-Zertifikat. Um den allgemeinen Namen des Zertifikats korrekt festzulegen, müssen Sie die FQDN-Umgebungsvariable in „docker/fqdn.env“ in den vollständig qualifizierten Domänennamen Ihrer Workstation ändern.

Wenn Sie PWA-Funktionen testen möchten, müssen Sie der Zertifizierungsstelle des Zertifikats für Ihre lokale Bereitstellung vertrauen. Der Einfachheit halber können Sie die crt-Datei von `http://<Your FQDN>:8080/ca.crt` herunterladen. Installieren Sie dieses Zertifikat im Trust Store Ihres Betriebssystems.
- Stellen Sie unter Windows sicher, dass Sie es im Speicher „Vertrauenswürdige Stammzertifizierungsstellen“ installieren.
- Doppelklicken Sie unter MacOS auf das installierte CA-Zertifikat in „Schlüsselbundzugriff“, erweitern Sie „Vertrauen“ und wählen Sie „Immer vertrauen“ für SSL.
- Firefox verwendet einen eigenen Trust Store. Um die Zertifizierungsstelle zu installieren, verweisen Sie Firefox auf „http://<Your FQDN>:8080/ca.crt“. Wenn Sie dazu aufgefordert werden, wählen Sie „Dieser Zertifizierungsstelle vertrauen, um Websites zu identifizieren“ und klicken Sie auf „OK“.
- Wenn Sie Chrome verwenden, müssen Sie Chrome neu starten, damit der Trust Store neu geladen wird (`chrome://restart`). Außerdem müssen Sie nach der Installation eines neuen Zertifikats den Speicher löschen (DevTools -> Application -> Clear storage -> Clear site data).

Bitte beachten Sie, dass die Zertifikate (CA- und Webserver-Zertifikat) nach einem Tag ablaufen.
Außerdem werden bei jedem Neustart des Nginx-Dockers neue Containerzertifikate erstellt.

Die Seite wird auf `https://<Your FQDN>:443` bereitgestellt.
   
## Deployment Notes
The client expects the server at http(s)://your.domain/server.

When serving the node server behind a proxy, the `X-Forwarded-For` header has to be set by the proxy. Otherwise, all clients that are served by the proxy will be mutually visible.

By default, the server listens on port 3000.

For an nginx configuration example, see `docker/nginx/default.conf`.

## Desktop App 
Note: if you are using Google Chrome, you can easily install Snapdrop PWA on your desktop by clicking the install button in the top-right corner.

If you are not using Chrome or Edge, you can install the [Snapdrop Desktop App](https://github.com/infin1tyy/snapdrop-desktop) built on top of Electrum. (Thanks to Infin1tyy!).


