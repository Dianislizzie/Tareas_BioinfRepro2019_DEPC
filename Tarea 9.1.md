<h2 id="tarea-9.1">Tarea 9.1:</h2>
<h2 id="ensamblaje-de-representación-reducida-de-genomas">Ensamblaje de representación reducida de genomas</h2>
<p>Diana Peláez Cajas</p>



<p><strong>INTRODUCCIÓN</strong></p>
<p>En la última década el desarrollo de secuenciación de ADN asociada a sitios de restricción (RADseq) ha permitido incrementar los estudios en genómica ecológica, evolutiva y de conservación, ya que brinda un rendimiento masivo para descubrir cientos o miles de marcadores genéticos polimórficos en todo el genoma en un experimento único, simple y rentable. Otras ventajas son que: brinda mayor profundidad de cobertura por locus, la secuenciación de un mayor número de muestras para un determinado presupuesto llegando a ser más económico que el análisis del genoma completo. Además, no requiere ninguna información genómica previa para los taxones que se estudian por lo tanto se puede aplicar en organismos modelo o no modelo (1)(2).</p>
<p>Sin embargo, estudios han demostrado que una de las limitantes para que RADseq pueda ser aplicado, es la gran cantidad de <em>missing data</em> que genera. Esto puede ocurrir por varios factores técnicos en el laboratorio como: la muestra que se analiza, la enzima de restricción utilizada, el tamaño de los fragmentos seleccionados y la variación en la cobertura de secuenciación y entre las muestras afectan el número de loci recuperados y otro factor es el análisis bioinformático utilizado para ensamblar los datos. Cabe mencionar que el ensamblado se puede realizar de novo o contra un genoma de referencia (3). Dentro de los programas para ensamblar datos generados por RADseq se encuentra PyRAD, que reúne locus RADseq alineados de novo para análisis filogenéticos a nivel de población, con un enfoque particular en el análisis de muestras altamente divergentes. PyRAD usa un algoritmo de agrupamiento de alineación global, que permite la incorporación de la variación de indel al identificar homología. PyRAD se distingue de estos programas por su velocidad, flexibilidad para analizar múltiples tipos de datos RADseq, su escalabilidad a conjuntos de datos extremadamente grandes y divergentes y su facilidad de uso(3). Identifica variaciones de tipo SNP e indels con protocolos en el laboratorio de RAD, ddRAD, GBS, NextRAD, RApture y los conjuntos de datos reunidos se crean en una variedad de formatos de salida, lo que facilita los análisis genómicos posteriores para los estudios genéticos y filogenéticos de la población. También incluye métodos para visualizar y analizar datos y resultados.</p>
<p><strong>Parámetros de ensamblaje</strong></p>
<p>En general hay valores predeterminados, pero he considerado como los parámetros más sensibles y que pudiesen influir en el resultado del ensamblado.</p>
<p><strong>clust_threshold</strong></p>
<p>Principalmente si se está realizando un ensamblaje de novo por lo tanto se ensamblará de acuerdo a la similitud entre las secuencias obtenidas y por lo tanto se agrupan al ser homólogas, este valor debe ser menor a 0,95 ya que estas secuencias podrían no agruparse debido a la presencia de Ns, indels, errores de secuenciación o polimorfismos.</p>
<p>Se optimizaría este parámetro en la línea 14 de ipyrad params file:</p>
<pre><code>0.90  _## [14] clust threshold set to 90%_

0.85  _## [14] clust threshold set to 85%_
</code></pre>
<p><strong>min_samples_locus</strong></p>
<p>De acuerdo a Huang et al, 2016 se sugiere no filtrar demasiado los <em>missing data</em> con aumentando el valor de <em>min_samples_locus</em> ya que a pesar de que las matrices de los datos tengan gran cantidad de <em>missing data</em> no afecta adversamente la precisión filogenética. Por lo tanto, no se seguiría la sugerencia de aumentar a 12 sino de 4 para mantener los <em>missing data.</em></p>
<pre><code>12 _## [21] create a min4 assembly_

4  _## [21] create a min4 assembly_
</code></pre>
<p><strong>DISCUSIÓN</strong></p>
<p>De acuerdo a los parámetros que considera ipyrad hay que considerar que lo que se busca principalmente en especies no modelo y en el ensamblaje de novo es la homologación de secuencias por lo tanto se debe evitar aumentar parámetros que puedan evitar la homologación de tales secuencias. Por otro lado, bajo la evidencia de estudios recientes no se debe tratar de eliminar la mayor cantidad de <em>missing data</em> ya que estos datos no intervienen en la precisión filogénetica y más bien se estaría al reducir o eliminar estos datos se afectaría los tipos de loci muestreados.</p>
<p>En particular, a medida que la tolerancia para los datos faltantes se vuelve más estricta, el espectro mutacional representado en los loci muestreados se trunca, de modo que los loci con las tasas de mutación más altas se excluyen de manera desproporcionada(4). Sugiriendo que las matrices más grandes (y más incompletas) contienen más información filogenética por nucleótido que sus contrapartes más pequeñas y completas(5).</p>
<ol>
<li>Andrews KR, Good JM, Miller MR, Luikart G, Hohenlohe PA. Harnessing the power of RADseq for ecological and evolutionary genomics. Nat Rev Genet [Internet]. 2016;17(2):81–92.</li>
<li>Rochette NC, Catchen JM. Deriving genotypes from RAD-seq short-read data using Stacks. Nat Protoc [Internet]. 2017;12(12):2640–59.</li>
<li>Eaton DAR. PyRAD: Assembly of de novo RADseq loci for phylogenetic analyses. Bioinformatics. 2014;30(13):1844–9.</li>
<li>Huang H, Lacey Knowles L. Unforeseen consequences of excluding missing data from next-generation sequences: Simulation study of rad sequences. Syst Biol. 2016;65(3):357–65.</li>
<li>Crotti M, Barratt CD, Loader SP, Gower DJ, Streicher JW. Causes and analytical impacts of missing data in RADseq phylogenetics: Insights from an African frog (Afrixalus). Zool Scr. 2019;48(2):157–67.</li>
</ol>

