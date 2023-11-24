# AirManagement - Use-Case Description Forecasting Energy consumption
Proiectul isi propune reducerea si predictia consumului de aer comprimat, utilizat in procesele de productie industriala.
Proiectul a fost impartit in doua zone:
1. Integrarea datelor (debit instant, presiune, temperatura, debit total consumat) de consum aer din zona de OT in zona de IT
2. Predictia consum (debit de aer total consumat)lui de aer utilizand arhitectura Convolutional Neuronal Networks(CNN) si Generative Adversarial Network (GAN)
![image](https://github.com/ro0tst/AirManagement/assets/93845063/fd3f6e59-ff78-4d0c-994e-ab557ed6bf3b)

Integrarea datelor dinOT in IT
![image](https://github.com/ro0tst/AirManagement/assets/93845063/1e91d86f-40aa-4ca9-b30d-da1798aa5872)
Pentru reducerea consumului de aer, am dorit sa integram in arhitectura de date, echipamentului industrial Air Management System (AMS), producator firma SMC.
Mai jos gasiti un link catre pagina producatorului
https://www.smcworld.com/webcatalog/en-jp/air-management-system/air-management-system/AMS_AB-E/#detail
Alegerea acestui produs a fost determinata de faptul ca, caracteristicile tehnice privind ingestia datelor, catre zona de IT, se fac pe protocolul OPC UA.
Accesul datelor, utilizand protocolul OPC UA, ne permite o independenta fata de controllerul master al utilzajului, pe care se instaleaza acest dispozitiv. In felul acesta, nu mai eram restrictionati de vechea arhitectura a datelor, din procesele industriale si de eventualele restrictii de securitate, impuse de producatorul utilizajului pe care vroiam sa optimizam.
Aceasta etapa a avut ca scop final ingetia datelor venite de la echipamentul Air Management System (AMS),  in timp real in platforma Google Cloud (Data Wharehouse - BigQuery) si utilizarea instrumentelor de BI (Looker Studio) pentru vizualizarea datelor.
Pe parcursul implementarii proiectului, a mai aparut o solicitare, venita de la un partener industrial, ca ingestia in timp real a datelor sa se faca on-primise, in MySQL.

Predictia consum.
Pentru predictia consumului am optat pentru o arhitectura de Depp Learning de tip Convolutional Neuronal Networks(CNN) si Generative Adversarial Network (GAN)
Motivul pentru care am adoptat aceasta directie a fost problema comuna, pentru adoptia algoritmilor de ML si anume datele necesare pentru antrenarea modelelor, date care in majoritatea cazurilor sunt fie insuficiente, fie irelevante pentru model. De cele mai multe ori aceste date de antrenament necesita timp îndelungat in colectarea lor ceea ce duce la ROI indelungat.Am utilizat arhitectura GAN pentru generarea de date realiste care sa imbogateasca setul initial de date. Similar cu consumul energetic, GAN-ul a fost util pentru a genera exemple suplimentare de debit de aer, astfel încât să avem un set de date mai diversificat și reprezentativ.
Alegerea arhitecturii CNN a fost determinata de :
Reprezentarea spațială a datelor: Am presupus ca datele vor avea o  distribuția în timp și spațiu a consumului de aer comprimat, iar CNN-urile pot fi eficiente în capturarea acestor relații spațiale. Straturile de convoluție pot ajuta la identificarea pattern-urilor spațiale și la învățarea caracteristicilor din aceste date.
Detectarea de tipare locale: CNN-urile sunt specializate în detectarea de tipare locale în date. Dacă există caracteristici locale semnificative în datele tale, cum ar fi variații bruște în consumul de aer comprimat în anumite regiuni sau intervale de timp, CNN-urile pot să le identifice eficient.
Extinderea setului de date prin generare: Cum setul nostru de date era limitat, GAN-urile (Generative Adversarial Networks) au putut pot fi integrate într-o arhitectură CNN pentru a genera exemple suplimentare realiste.

4. **Flexibilitatea în manipularea datelor spațiale**: CNN-urile sunt potrivite pentru date spațiale, cum ar fi imagini sau distribuții spațiale. Dacă datele tale pot fi reprezentate sub formă de matrice (cum ar fi matricea de imagini), CNN-urile sunt adaptate pentru manipularea acestui tip de date.

5. **Reprezentarea ierarhică a caracteristicilor**: CNN-urile sunt capabile să învețe ierarhii de caracteristici, de la cele simple la cele complexe. Această abordare ierarhică poate fi utilă în identificarea diferitelor niveluri de influență asupra consumului de aer comprimat.

Este important să menționezi că alegerea arhitecturii depinde și de specificul datelor tale și de complexitatea relațiilor pe care încerci să le capturezi. Experimentarea și evaluarea multiplelor arhitecturi te vor ajuta să determini ce funcționează cel mai bine pentru setul tău de date și pentru obiectivele tale de forecasting.
