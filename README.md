# Demodulador neuronal QAM

Demo interactiva de l'assignatura *Integració de la IA en Telecomunicacions* (URV, Grau de Telecomunicacions, 4t curs).

Una xarxa neuronal (MLP) s'entrena directament al navegador per demodular una constel·lació QAM amb soroll, i es compara amb el detector clàssic de mínima distància.

**Demo en línia:** `https://<organització>.github.io/demo-qam-neuronal/`

## Què permet fer

- Triar la modulació (QPSK, 16-QAM, 64-QAM) i l'Es/N0 (0–30 dB).
- Afegir distorsions de canal: amplificador no lineal (model de Saleh), soroll de fase i desequilibri IQ.
- Configurar la xarxa: capes ocultes, neurones per capa, activació, taxa d'aprenentatge i nombre de mostres d'entrenament.
- Veure en temps real les regions de decisió apreses i comparar la SER de la xarxa amb la del detector de mínima distància i la teòrica AWGN.
- Obtenir la corba SER vs SNR amb la xarxa entrenada, per estudiar-ne la generalització.
- Provar quatre escenaris preparats per a classe: soroll gaussià pur, amplificador saturat, soroll de fase i poques dades.

Cada control té una ajuda contextual (icona «i») i la pàgina inclou un apartat «Com funciona».

## Com funciona per dins

Tot és JavaScript pur en un sol fitxer, `index.html`, sense llibreries ni servidor:

- **Dades**: es generen al navegador. Símbol aleatori → distorsió del canal → soroll gaussià (Box-Muller).
- **Xarxa**: MLP amb entrada (I, Q), capes ocultes ReLU o tanh i sortida softmax amb M classes.
- **Entrenament**: entropia creuada, retropropagació feta a mà i optimitzador Adam, amb mini-lots de 64 mostres.
- **Bucle**: `requestAnimationFrame` fa 10 passos d'entrenament per fotograma i redibuixa les regions de decisió periòdicament.
- **Avaluació**: SER sobre 10 000 mostres de prova independents.

## Executar-la en local

Obre `index.html` amb qualsevol navegador. No cal instal·lar res.

## Publicació

El workflow `.github/workflows/pages.yml` la publica a GitHub Pages cada vegada que es fa push a `main`.

Configuració inicial, només un cop: **Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Estructura

```
.
├── index.html                  # la demo sencera
├── .github/workflows/pages.yml # publicació automàtica a GitHub Pages
├── .nojekyll
├── LICENSE
└── README.md
```

## Llicència

MIT. Vegeu [LICENSE](LICENSE).
