## Design and Fabrication of an Automated Discharge Collection Unit of a Synthetic Hdyro-Experimental Machine

Latex sources

### Usage
Run ```renamef``` in the source directory to rename the output file.
```bash
    renamef
``` 

### Removing redundant pictures
Reduce documentation raw size
```bash
mkdir temp_pictures;
grep -oE '\{Figures/[a-zA-Z]+\.[a-zA-Z]+\}' Files/*     | sed 's/^[^{]*{\([^{}]*\)}.*/\1/'  | xargs cp -t  temp_pictures/  ;
cp -i Figures/JKUAT_logo.png  temp_pictures/ ;
rm -rf Figures/  ;
mv temp_pictures/  Figures/
```

### Reduce image sizes 

```bash
# find Figures/ -name "*.png" -or -name "*.PNG"
mkdir temp_pictures2 ; 
# rename all *.PNG to *.png
for file in $(find Figures/ -name "*.PNG"); do 
    mv -- "$file" "${file%.PNG}.png"
done
# Compress all png files
for i in $(find Figures/ -name "*.png"); do
  R_FILE=$(echo $i |  sed 's/.*\///')
  convert "$i" -resize 1200x1200 "temp_pictures2/${R_FILE%.png}.jpg";
done
rm -rf Figures/;
mv temp_pictures2/  Figures/;
```