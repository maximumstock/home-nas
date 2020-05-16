# DIY Home NAS 2020

Personal notes and gathered information on building a simple home NAS for myself.

## Background

For a while I've had the idea of acquiring a simple home NAS for my backup and file/media
storage needs.
While there are lots of products on the market that provide such functionality without too
much hassle to setup and maintain, I always liked the idea of tinkering myself.
Therefore, to eventually reach my dream of my low-power home NAS - and to fight the boredom
during Covid-19 - I set out to gather some insight on how to realise it.

In this repository, I try to document my thought process and bits of information I gather
along the way.

## Requirements

My actual requirements are rather basic:

- Storing Time Machine backups
- Supporting a growing RAW photo collection
- Decent throughput
  - With 125 MB/s being the Gbit Ethernet limit, I'd like to reach 100-110 MB/s
- Streaming some media to terminal devices

What I do not need and probably never will:

- Transcoding
  - Sure, maybe a small 1080p video here and there, but nothing fancy
- Running 24/7

# Hardware

## Mini-ITX Setup

- Case: [Fractal Design Node 304](https://www.mindfactory.de/product_info.php/Fractal-Design-Node-304-Wuerfel-ohne-Netzteil-schwarz_819144.html) (86.31 €)
- RAM: [16GB Crucial CT16G4SFD824A DDR4-2400 SO-DIMM CL17](https://www.mindfactory.de/product_info.php/16GB-Crucial-CT16G4SFD824A-DDR4-2400-SO-DIMM-CL17-Single_1133874.html) (86.96 €)
- MB: [ASRock J5005-ITX SoC So.BGA Dual Channel DDR4 Mini-ITX Retail](https://www.mindfactory.de/product_info.php/ASRock-J5005-ITX-SoC-So-BGA-Dual-Channel-DDR4-Mini-ITX-Retail_1229238.html) (118.65 €)
- PSU 2:
  - [SilverStone SST-ST30SF v 2.0](https://www.amazon.de/SilverStone-SST-ST30SF-2-0-fl%C3%BCsterleises-PC-Netzteil/dp/B01LY7UZNE/ref=sr_1_1?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&keywords=SILVERSTONE%2BSFX%2BST30SF%2B300W&qid=1585223613&sr=8-1&th=1) (52.90 €)
    [Ref](https://www.reddit.com/r/HomeServer/comments/a3ysbe/picopsu_vs_atx_psu_for_powering_small_server_with/eba9ohv/)
- Storage:
  - HDD: 2x [Western Digital Red 4 TB](https://www.mediamarkt.de/de/product/_wd-red%E2%84%A2-nas-festplatte-bulk-2629343.html) (2x 109 €)
  - OS: [WD Green 120GB Interne SSD (2,5 Zoll) SATA](https://www.amazon.de/gp/product/B076XWDN6V/ref=ox_sc_act_title_1?smid=A3JWKAKR8XB7XF&psc=1) (28.99 €)

Total: ~593 €

Optional power supply:

- [PicoPSU-150-XT 150W 12V DC-DC ATX Netzteil/Power Supply](https://www.amazon.de/gp/product/B0045IXKTQ/ref=ox_sc_act_title_4?smid=A21ISB9LUWIYXR&psc=1) (39.95 €)
- [LEICKE ULL Netzteil 12V 12.5A 150W](https://www.amazon.de/gp/product/B00YXXAG7C/ref=ox_sc_act_title_5?smid=A2Z54WBF904K0X&psc=1) (39.99 €)
- Sata Power Splitter: [deleyCON 0,15m S-ATA Strom-Adapter Y-Adapter](https://www.amazon.de/gp/product/B01F24PMV0/ref=ox_sc_act_title_3?smid=A326X3AG3XUTK4&psc=1) (8.99 €)

A PicoPSU is meant to work more efficiently at low idle consumption, which fits this kind of NAS setup.
However, on startup, HDDs need quite a bit of juice to actually power up and start spinning.
During research, some numbers I found were like 30-40W per HDD on startup + whatever the remaining
components require.

If you're planning on supporting 4-8 3.5" HDDs, then a PicoPSU is most likely not gonna suffice.

Side note: Off-the-shelf solutions seem to use PicoPSUs or something similarly efficient, but
end using [staggerd disk spin-up](https://en.wikipedia.org/wiki/Spin-up) to reduce the total
wattage needed during initial startup.

### Advantages

- Extendable Storage
  - 4 SATA 3 ports by default; 4 additional SATA 3 ports possible via PCIe 2.0 card
  - Up to 6x3.5" drive bays
- RAM Flexibility
  - Up to 32GB RAM in total
  - 2x4GB/8GB RAM possible for smaller budget
- Much more CPU performance and RAM than SBCs and even off-the-shelf solutions, eg. Sonology
- Still relatively low power usage considering performance

### Disadvantages

- Higher price than SBC 2-bay setups
- Higher power usage than SBC setups

### References

#### Mini-ITX

- https://www.reddit.com/r/HomeServer/comments/ahq5e7/my_private_15w_allinone_homeserver_and_media/
- https://www.technikaffe.de/anleitung-178-eigenbau_nas_anleitungen_fuer_4_bis_16_festplatten_auf_einen_blick/
- https://www.reddit.com/r/HomeServer/comments/f6lj8r/hardware_choice_for_basic_nas_on_a_budget/
- https://www.speicher.de/arbeitsspeicher-blog/32gb-arbeitsspeicher-asrock-j4105-itx

#### SBC

- https://forum.openmediavault.org/index.php?thread/27301-nas-based-on-nanopi-m4-and-sata-hat/&pageNo=1
