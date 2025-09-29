# SoniDB
SoniDB – En ljudbaserad vektordatabas för maskininlärning

🧠 Vision
Att skapa en ny typ av databas där vektorer lagras som ljud, distribueras via ljudoptimerade protokoll, och används direkt i maskininlärningsmodeller – med målet att överträffa traditionella databaser som CosmosDB i prestanda, skalbarhet och streamingeffektivitet.

🔧 Teknisk Arkitektur
1. Vektor → Sonifiering → FLAC
    Varje vektor konverteras till ett ljudsegment via frekvenskodning, amplitudmodulering eller pulslängd.
    Segmentet sparas som en FLAC-fil för lossless komprimering och exakt återställning.
2. Metadata & Index
    Metadata bäddas in i FLAC-filen (t.ex. vektor-ID, kodningsmetod, hash).
    En extern indexfil (JSON eller binär) mappar vektor-ID till fil, tidsposition och hash.
    Indexfilen fungerar som en SFV-liknande struktur för dataintegritet och snabb lookup.
3. Streamingmotor
    FLAC-filer streamas via HTTP, WebRTC eller HLS.
    Mottagaren extraherar metadata och rekonstruerar vektorer i realtid.
    ML-modeller kan lyssna direkt på strömmen och använda vektorer för inference.
4. FXP-distribution
    FXP används för att synka FLAC-filer mellan noder utan att belasta klienten.
    Ger blixtsnabb global spridning av vektordata – perfekt för ML i distribuerade miljöer.

⚡ Prestandamål
Metrik	Mål
Ingest speed	>1000 vektorer/s
Retrieval latency	<10 ms per vektor
Streaming throughput	>10 MB/s
Distribution time	<5 min globalt via FXP
Storage efficiency	<1 KB per vektor (FLAC + metadata)

📦 Funktioner
    InsertVector(vec []float64) – konverterar och sparar vektor som FLAC
    StreamVector(id string) – streamar ljudsegment för given vektor
    BuildIndex() – uppdaterar indexfilen med nya vektorer
    VerifyIntegrity() – kontrollerar hash mot FLAC-innehåll
    SyncNode(target string) – FXP-baserad synk mellan noder

🧪 Användningsområden

    ML inference i realtid via ljudström
    Distribuerad träning med vektorer som ljud
    Edge computing där ljud är enklare att streama än JSON

    Datasäkerhet via ljudbaserad steganografi och hashverifiering
