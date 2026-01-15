Foto procesada por OpenDroneMap para ortogonalizar las fotos (quitar la perspectiva) y así poder mapear en OSM.

Aquí se sube en caso que no esté disponible OpenAerialMap. Igualmente sirve publicarla aquí para poder subirla a la plataforma OAM, por medio de URL.

Debido a que las ortofotos son archivos de gran tamaño, se puede dividir el archivo, comprimiédolo por partes del mismo tamaño. Con el siguiente comando se comprime un archivo tiff grande creando varios archivos de 10 MB. Se recomienda crear el zip en la raiz de este repositorio, ya que el script que mueve todo lo hace automático desde esa ubicación.

```
zip -s 10m ortofoto.zip ortofoto.tif
```

Una vez se tienen varios archivos pequeños se suben a GitHub. Se recomienda tener el repositorio sin cambios pendientes por subir.

```
mv ../ortofoto.zip .
git add ortofoto.zip
git commit ortofoto.zip -m "Prime archivo del zip"
git push
# Obtiene el número que representa la última parte.
MAX_NUM=$(ls -1 ortofoto.z?? | grep -v ortofoto.zip | tail -1 | awk -F.z '{print $2}')
for i in $(seq -f %02g 1 ${MAX_NUM}) ; do
 mv ../ortofoto.z${i} . ;
 git add ortofoto.z${i} ;
 git commit ortofoto.z${i} -m "Parte zip" ;
 git push ;
done
```

NOTA: Este tipo de foto ya casi no se publica en el repositorio GitHub por su gran tamaño, lo cual es restringido por los límites de GitHub. En contraste, se prefiere publicar las fotos en OpenAerialMap, servicio que permite usarlas en editores como JOSM sin necesidad de descargarlas.
