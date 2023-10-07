## O histórico do meu lastfm
 
![image](https://github.com/nadjapereira/lastfm/assets/11997614/6e7a3750-c52e-40b3-b30c-6423b8619144)


A **_lastfm_** é a rede social mais antiga que eu tenho. Eu criei meu perfil em 2008 e até hoje faço o scrobble das músicas. Os primeiros usos eram de músicas baixadas, depois vieram os streamings como Spotify e agora, majoritariamente, os dados são do **Youtube Music**. A análise abaixo é para ver se descobria alguma música antiga que eu gostava e nunca mais a ouvi, além de checar se o meu gosto musical continua o mesmo ao longo destes 15 anos.  

Passo a passo da análise
1. Download da base usando esse site: [Last.fm data export](https://mainstream.ghan.nl/export.html)
2. Na limpeza eu coloquei '1970' em dados desconfigurados de '2008', excluí códigos do artista_mbid e o album_mbid, separei o UTC_Time entre a data (importante) e o horário (pouco importante)
5. O youtube ainda tem alguns problemas relacionados a indexação de algumas músicas, portanto fiz exclusões de vídeos não musicais.
6. Usei o SQLite para a análise  </br> 
</br>

**Toda a minha base musical tem 40.780 linhas e eu dei play em mais de 8 mil artistas diferentes** 
````
SELECT * from lastfm 
````

**As músicas que mais "escutei" por ano** e **Os picos de scrobbles**</br> 

```` 
SELECT strftime('%Y', utc_time) as ano,
COUNT (*) as quantidade
FROM lastfm
group by strftime('%Y', utc_time)
order by ano
```` 

A maior surpresa foi quando eu gerei um gráfico no excel e achei interessante essa queda brusca a partir de 2014, a época em que eu comecei a usar antigo Google Music que não fornecia (ou eu não sabia) streaming para o lastfm. Em 2016 que eu passei a usar o spotify e o scrobble das músicas voltaram a subir. 

![image](https://github.com/nadjapereira/lastfm/assets/11997614/2e12aa58-4d8e-49e7-9eb4-c837b0c9f4d9)


Em 2020 ocorreu uma nova queda porque eu parei de usar o spotify e passei a usar o youtube com muita frequência (tinha scrobble, mas eu não fazia). Usava também o soundcloud que ainda não possui uma conexão perfeita com o lastfm. Os maiores picos de streamings são da era 'download de música' em 2010 e 'spotify'/apple music no final de 2016 e, principalmente, em 2017. 

**O primeiro lugar completamente inusitado** </br>
Chiddy Bang com Bday é o primeiro lugar da lista, uma música que eu não faço ideia de ter escutado (???). Ao fazer a análise, não lembrava dela e dei play, mas sensação que tive foi de ter ouvido pela primeira vez e achei tão que estranho porque eu não gostei da música. Eu devo ter deixado ela rodar no streaming por alguma razão. As listas das músicas das mais escutadas nesses 15 anos tem muita coisa surpreendente, tipo 220 scrobbles de "Lua de Cristal" da Xuxa (????). Eu não faço ideia do motivo de uma música da minha infância ter sido tão ouvida em 2015. 

```` 
SELECT strftime('%Y', utc_time) as ano, artist, track,
COUNT (*) as quantidade
FROM lastfm
group by strftime('%Y', utc_time)
order by quantidade DESC;
```` 

![image](https://github.com/nadjapereira/lastfm/assets/11997614/b516f76c-69aa-4ecc-a00d-5aca4dcacab4)


Foi realmente surpreendente fazer essa análise e é muito legal perceber que o meu gosto é mais ou menos o mesmo: muita música pop, dance music, algum hiphop e MPB. Com a mais absoluta certeza farei novamente este tipo de análise. É um exercício muito interessante revisitar a própria memória. 

Nadja Pereira

Referência: [Introdução a Linguagem SQL - Abordagem prática para iniciantes](https://amzn.to/46yCnnS)


