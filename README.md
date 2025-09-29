# Proyecto Final – Regresión Lineal y Regularización

## Integrantes
- JOEL MATEO MANRIQUE VELASQUEZ
- LUIS ENRRIQUE PEREZ RAMOS

---

## 📌 Diferencias observadas entre OLS, Ridge y Lasso

### California Housing
- **OLS (Closed-form)**: Captura la relación lineal base y obtiene buen desempeño, pero es sensible a la multicolinealidad entre las variables y puede sobreajustar si hay correlaciones fuertes.
- **Ridge**: Introdujo regularización que redujo la varianza del modelo. Observamos que los coeficientes se encogieron de manera más uniforme, logrando un mejor equilibrio entre sesgo y varianza.
- **Lasso**: Mantuvo un α muy pequeño (≈0.001), lo que indica que apenas aplicó penalización. Esto se debe a que ninguna variable fue claramente redundante o innecesaria, por lo que el modelo se comportó casi igual a OLS.

### Bike Sharing (hour.csv)
- **OLS**: Ajustó bien los datos, pero no manejó del todo la complejidad asociada a la estacionalidad y los patrones horarios.
- **Ridge**: Seleccionó un α bastante alto (≈49.4), lo que muestra que una regularización fuerte ayudó a controlar la alta correlación entre variables temporales (hora, día, estación). Obtuvo un MSE ≈19380.
- **Lasso**: Escogió un α muy bajo (≈0.13), mostrando que prefirió no eliminar variables. Su MSE fue prácticamente igual al de Ridge (≈19379), lo que indica que ambos modelos se comportaron de forma muy similar, aunque con distinta fuerza de regularización.

---

## 📌 Efecto de la tasa de aprendizaje en Gradient Descent

### California Housing
- Con una tasa de aprendizaje **muy pequeña**, el descenso de gradiente converge de forma estable, pero muy lentamente.  
- Con una tasa **más alta**, el costo disminuye mucho más rápido, aunque si es demasiado grande, el algoritmo puede oscilar o divergir.  
- En este dataset, se observó que un valor intermedio permitió alcanzar resultados comparables al OLS cerrado en menos iteraciones.

### Bike Sharing
- Debido a la mayor complejidad y número de observaciones, la elección del learning rate fue aún más importante.  
- Un valor demasiado alto llevó a oscilaciones en la curva de costo, mientras que valores moderados lograron converger a un error cercano al alcanzado por los métodos cerrados y regularizados.

---

## 📌 Influencia de k-Fold Cross-Validation en la elección de la regularización

### California Housing
- El uso de **k=5 folds** permitió estimar de manera más robusta el desempeño de Ridge y Lasso en distintos subconjuntos de datos.  
- Ridge obtuvo un α ≈3.7, lo que indica que una regularización moderada mejoraba el ajuste.  
- Lasso seleccionó un α ≈0.001, mostrando que no era necesario eliminar variables en este dataset.

### Bike Sharing
- En este caso, la validación cruzada encontró un **α mucho más alto para Ridge (≈49.4)**, evidenciando la necesidad de un control fuerte frente a la multicolinealidad y los patrones estacionales.  
- Lasso, en contraste, mantuvo un α bajo (≈0.13), indicando que ninguna variable fue eliminada, aunque la penalización mínima fue suficiente para estabilizar el modelo.  
- En ambos casos, la validación cruzada fue clave para ajustar la fuerza de regularización según la complejidad y redundancia de las características.

---

## 📌 Conclusión General
- En **California Housing**, la regularización apenas mejoró el desempeño respecto a OLS, porque el dataset no requería una fuerte penalización.  
- En **Bike Sharing**, Ridge necesitó un α grande para estabilizar el modelo frente a la alta correlación de variables temporales, mientras que Lasso casi no eliminó predictores, pero alcanzó un error similar.  
- La validación cruzada fue esencial para adaptar la regularización a cada dataset, mostrando cómo un mismo método puede comportarse distinto según la estructura de los datos.  
- El gradiente descendente confirmó la importancia de elegir adecuadamente la tasa de aprendizaje para garantizar convergencia sin inestabilidad.
