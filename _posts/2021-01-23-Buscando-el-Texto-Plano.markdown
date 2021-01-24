---
layout: post
title:  "Buscando el Texto Plano"
date:   2021-1-23 20:22:36 -0500
categories: tech
---
No soy un experto en seguridad, pero me gusta el tema. Es por eso que hace años escucho el podcast [Security Now](https://www.grc.com/securitynow.htm) todas las semanas y me suscribo a algunas noticias. Creo que Steve Gibson hace un buen trabajo en aterrizar los temas complejos de manera que otros no ten expertos, como yo, los podamos entender.

En el último episodio el anfitrión, conversando sobre seguridad en aplicaciones de mensajería, hace un comentario muy bueno que me permito reproducir aquí:

*If you look at the packets moving across today's Internet, unlike the Internet of 15 years ago, when we began this podcast,  all you will ever see today is packets full of noise.  Just 100% random bits of noise.  Today it's all noise.  It's all encrypted.  And no one bothers looking at it because anyone who wants to know what's in those packets also knows quite well that the encryption problem has long since been solved and that none of that noise on the wire can be decrypted.  The apocryphal story of the infamous bank robber Willie Sutton applies here.  The story goes that a reporter once asked Willie why it was that he robbed banks.  And Willie was said to reply, "Because that's where the money is."  Updating the story to 2021, a non-technical supervisor at the NSA might ask one of their top technical managers why all of the agency's work has been diverted to investments in keystroke logging, to which the technical manager would reply, "Because that's where the plaintext is."*

Y es que es la verdad, la seguridad más avanzada del mundo es tan débil como su más débil eslabón. De nada sirve tener las conexiones muy cifradas para que el mensaje en tránsito sea imposible de leer, si luego en los dispositivos se encuentra en texto plano.

Algo parecido lo observo con varias empresas que invierten mucho esfuerzo en tener datos cifrados antes de subirlos a bases de datos donde existe ya un cifrado por defecto, con el màximo control de accesos, comnsumiendo muchos recursos... solo para que al final de la cadena se exporte todo como un archivo de texto porque eso es lo que se necesita para un reporte o un sistema core. Si alguien quiere ver esos datos, pues va directamente a ese archivo, that's where the plaintext is.