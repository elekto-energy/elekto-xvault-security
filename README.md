elekto-xvault-security

ELEKTO-XVault Security Layer är säkerhetsmotorn för ELEKTO-plattformen. Den fungerar som ett Root-of-Trust-lager som validerar, loggar och skyddar alla kommandon och dataflöden i ett distribuerat mikronät. Systemet ger stöd för attesterade noder, signerade snapshots, WORM-loggning, tokenbaserad åtkomstkontroll, AI-baserad intrångsdetektion samt PUF-fingeravtryck via CableDNA och MetalDNA.

Översikt av funktioner

XVault Security Agent
Den centrala säkerhetsmodulen som tar emot, analyserar och godkänner eller avvisar alla säkerhetskritiska operationer i systemet.

Snapshot Engine
Skapar signerade snapshots med monotona räknare och TTL. Säkerställer att mikronätet kan återgå till ett verifierat och konsekvent tillstånd vid ö-drift eller vid återanslutning till nätet.

WORM Log Engine
Oföränderlig append-only loggkedja baserad på hashkedjor. Används för revision, spårbarhet, forensik och upptäckt av manipulation.

Token Protection Engine
Implementerar ELEKTO-tokenmodellen (1 token = 1 kWh). Styr åtkomst till funktioner baserat på tokenregler, roller och giltighet.

Attestation Engine
Validerar att noder är äkta och oförändrade. Stöd för TPM/HSM-simulering samt fysiska PUF-tekniker via CableDNA (impedansprofil) och MetalDNA (elektromagnetisk signatur).

Intrusion Detection
AI-baserad modulanomali- och intrångsdetektion som flaggar misstänkta händelser, felaktiga beteendemönster eller potentiell tampering.

NetGuard
Granskar kommandon och trafik som rör SCADA, IoT-enheter, EV-laddare och andra noder i mikronätet.

CableDNA / MetalDNA Hooks
Förberedda moduler för fysiska komponentfingeravtryck av kablar och metalldelar för att upptäcka utbytta, manipulerade eller förfalskade komponenter.

Projektstruktur
xvault_security/
├── xvault_security_agent.py
├── attestation_module.py
├── snapshot_module.py
├── wormlog_module.py
├── token_protection_module.py
├── policy_module.py
├── intrusion_module.py
├── netguard_module.py
├── cabledna_module.py
├── metaldna_module.py
└── init.py
xvault_security_agent.py – huvudmotorn
attestation_module.py – attestering och PUF-stöd
snapshot_module.py – snapshotsystem
wormlog_module.py – immutable WORM-logg
token_protection_module.py – tokenbaserad åtkomstkontroll
policy_module.py – laststyrningsregler och prioritetssystem
intrusion_module.py – intrångsdetektion
netguard_module.py – nätverkskontroll
cabledna_module.py – PUF-profil för kablar
metaldna_module.py – PUF-profil för metallkomponenter
init.py – paketinitiering

Installation

Klona repository
git clone https://github.com/elekto-energy/elekto-xvault-security

cd elekto-xvault-security

Lägg till sökväg i Python
sys.path.append("D:/EVE11/projects/xvault_security")

Användning i EVE14-terminalen

xvault snapshot create 30
xvault snapshot verify
xvault worm append "Start"
xvault worm read
xvault attestation attest inverter01
xvault token validate ELEKTO-123
xvault token gate ELEKTO-123 start_charger
xvault intrusion scan
xvault intrusion tamper
xvault netguard inspect ev_charger01
xvault cabledna run
xvault metaldna run

Hur systemet fungerar

IntentParser identifierar att kommandot tillhör XVault.

ActionRouter skickar kommandot till XVault Security Agent.

XVault analyserar tokenregler, attestering, snapshotstatus, intrångsmönster och policylager.

Är säkerhetsläget avstängt (security_enabled = False) körs systemet i säkert demo-läge där allt tillåts men loggas.

Är säkerhetsläget aktiverat (security_enabled = True) tillämpas strikt enforcement.

Händelser loggas i WORM-loggen och kan inte ändras i efterhand.

Roadmap

PUF-fingeravtryck via CableDNA och MetalDNA
Multi-attestation (tvåmannaregel)
Säkra OTA-uppdateringar med rollback-skydd
Distribuerade XVault-kluster för hög redundans
Zero-knowledge proofs för energireserver
Utökad realtidsbaserad AI-intrångsdetektion

Licens

Copyright 2025 Organiq Sweden AB
Alla rättigheter förbehållna. Ingen vidareanvändning eller distribution utan skriftligt tillstånd.

Maintainer
Joakim Eklund, Organiq Sweden AB / ELEKTO Energy
