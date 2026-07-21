# Dashboard inmobiliario — precios de mercado

Visor de **precios efectivos de compraventa** (SII, Formulario 2890, 2015-2025) sobre la
misma plataforma territorial que el visor público de uso de suelo.

> ⚠️ **Repositorio privado.** Contiene la base de compraventas y los indicadores derivados.
> El visor público (uso de suelo, demografía, movilidad) vive en
> `romedinag-tech/ciudades_y_tendencias_de_Chile` y **no** incluye estos datos.

## Cómo se genera

No se edita aquí. Esta carpeta es un **destino de despliegue**: se regenera con

```
python proyecto_nacional/scripts/deploy.py inmobiliario
```

desde el proyecto de análisis. La fuente única de ambos dashboards es
`proyecto_nacional/web/`; el módulo de mercado se enciende con `data/site.json`.
El despliegue público excluye `data/mercado/`, apaga el módulo, recorta el marcado de la
pestaña y **audita** el resultado antes de terminar.

Autor: Rodrigo Medina González — Universidad de Concepción
