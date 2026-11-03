
# Memory and Storage Latency

## Part 1: L1 Cache, RAM, and SSD

L1 cache, RAM (DRAM), and SSDs operate at vastly different scales of performance, with latencies spanning from fractions of a nanosecond to tens of thousands of nanoseconds. The table below shows typical access latencies for modern desktop and server systems across these three layers of the memory hierarchy.

| Component | Typical Latency (ns) | Human-Scale Equivalent | Relative to L1 |
|-----------|----------------------|------------------------|----------------|
| L1 Cache | ~0.5 to 1 ns | 1 second | 1x (baseline) |
| System RAM (DRAM) | ~50 to 100 ns | ~1.5 minutes | ~100x slower |
| NVMe SSD (random read) | ~50,000 to 150,000 ns (50–150 µs) | ~1.7 days | ~150,000x slower |

### Key Takeaways

- **L1 cache (the core's desk):** Built directly into the CPU core using expensive, low-density SRAM. It runs at the same clock speed as the processor, taking only 3–5 CPU cycles to fetch data.
- **RAM (the room):** Uses higher-density DRAM located outside the CPU chip. Moving data across the motherboard bus adds significant overhead, requiring roughly 200–320 clock cycles to return a request.
- **NVMe SSD (the warehouse):** Much faster than mechanical hard drives, but flash storage must still cross the PCIe bus and go through solid-state controller lookup tables, which makes latency jump significantly.

### Further Exploration

- Latencies of intermediate layers such as L2 and L3 caches
- How sequential vs. random reads change these numbers
- How DDR5 memory timings affect real-world RAM latency

## Part 2: From L1 Cache to Network

Expanding the latency hierarchy covers everything from the CPU core to a global network request, spanning nine orders of magnitude. The table below fills in the gaps, including intermediate CPU caches, mechanical drives, and network boundaries.

| Component / Operation | Typical Latency (ns) | Human-Scale Equivalent | Relative to L1 |
|-----------------------|----------------------|------------------------|----------------|
| L1 Cache | ~0.5 to 1 ns | 1 second | 1x (baseline) |
| L2 Cache | ~3 to 4 ns | 4 seconds | ~4x slower |
| L3 Cache (shared) | ~12 to 20 ns | 20 seconds | ~20x slower |
| System RAM (DRAM) | ~50 to 100 ns | 1.5 minutes | ~100x slower |
| NVMe SSD (random) | ~50,000 ns (50 µs) | 14 hours | ~50,000x slower |
| SATA SSD (random) | ~150,000 ns (150 µs) | 1.7 days | ~150,000x slower |
| Rotational HDD (seek) | ~10,000,000 ns (10 ms) | 4 months | ~10,000,000x slower |
| LAN / local network | ~1,000,000 ns (1 ms) | 11.5 days | ~1,000,000x slower |
| Internet (edge / CDN) | ~10,000,000 ns (10 ms) | 4 months | ~10,000,000x slower |
| Internet (cross-Atlantic) | ~75,000,000 ns (75 ms) | 2.4 years | ~75,000,000x slower |

### Key Latency Milestones

- **On-chip layers (L1 to L3):** L1 and L2 are dedicated to individual CPU cores. L3 is larger, shared across all cores on a die, and acts as the final buffer before the CPU must leave the chip to fetch data.
- **Microsecond barrier (storage):** Moving from RAM to an NVMe SSD leaves processor clock cycles behind and enters hardware bus transfers. The jump from 1.5 minutes (RAM) to 14 hours (NVMe) in human-scale terms shows why disk I/O bottlenecks applications.
- **Network boundary:** A single rotation of a mechanical hard drive platter takes roughly as long as sending a packet to a nearby regional network server (~10 ms). Crossing an ocean over fiber-optic cable pushes latency into high milliseconds because light travels more slowly through glass.

## Sources

- Techcompare: *Memory Latency Numbers: L1 Cache to HDD* (www.techcompare.app)
- Stephen Blum, YouTube: *Latency Network vs SSD vs Memory vs Cache*
- GitHub: *Latency Numbers Every Programmer Should Know* (values based on ~2012 measurements)