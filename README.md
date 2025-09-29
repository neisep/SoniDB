# SoniDB
SoniDB – En ljudbaserad vektordatabas för maskininlärning

🧠 Vision
Att skapa en ny typ av databas där vektorer lagras som ljud, distribueras via ljudoptimerade protokoll, och används direkt i maskininlärningsmodeller med målet att överträffa traditionella databaser som CosmosDB i prestanda, skalbarhet och streamingeffektivitet.<br>

🔧 Teknisk Arkitektur<br>
1. Vektor → Sonifiering → FLAC<br>
    Varje vektor konverteras till ett ljudsegment via frekvenskodning, amplitudmodulering eller pulslängd.<br>
    Segmentet sparas som en FLAC-fil för lossless komprimering och exakt återställning.<br><br>
2. Metadata & Index<br>
    Metadata bäddas in i FLAC-filen (t.ex. vektor-ID, kodningsmetod, hash).<br>
    En extern indexfil (JSON eller binär) mappar vektor-ID till fil, tidsposition och hash.<br>
    Indexfilen fungerar som en SFV-liknande struktur för dataintegritet och snabb lookup.<br><br>
3. Streamingmotor<br>
    FLAC-filer streamas via HTTP, WebRTC eller HLS.<br>
    Mottagaren extraherar metadata och rekonstruerar vektorer i realtid.<br>
    ML-modeller kan lyssna direkt på strömmen och använda vektorer för inference.<br><br>
4. FXP-distribution<br>
    FXP används för att synka FLAC-filer mellan noder utan att belasta klienten.<br>
    Ger blixtsnabb global spridning av vektordata – perfekt för ML i distribuerade miljöer.<br><br>

⚡ Prestandamål<br>
Metrik	Mål<br>
Ingest speed	>1000 vektorer/s<br>
Retrieval latency	<10 ms per vektor<br>
Streaming throughput	>10 MB/s<br>
Distribution time	<5 min globalt via FXP<br>
Storage efficiency	<1 KB per vektor (FLAC + metadata)<br>
<br>
📦 Funktioner<br>
    InsertVector(vec []float64) – konverterar och sparar vektor som FLAC<br>
    StreamVector(id string) – streamar ljudsegment för given vektor<br>
    BuildIndex() – uppdaterar indexfilen med nya vektorer<br>
    VerifyIntegrity() – kontrollerar hash mot FLAC-innehåll<br>
    SyncNode(target string) – FXP-baserad synk mellan noder<br><br>

🧪 Användningsområden<br><br>
    ML inference i realtid via ljudström<br>
    Distribuerad träning med vektorer som ljud<br>
    Edge computing där ljud är enklare att streama än JSON<br>

    
