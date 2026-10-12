# Synthetic Task Flow Graphs for Latency-Focused Task Allocation in Fog-Edge-Cloud Systems

This repository provides a synthetic dataset generator for evaluating latency-oriented task allocation strategies in fog-edge-cloud environments. The generated graphs are modeled as directed acyclic graphs (DAGs) with a realistic mix of:

- few large computational tasks
- many small tasks
- heterogeneous computation costs across resource tiers
- communication dependencies between tasks
- fog, edge, and cloud resource profiles

The goal is to support research on task mapping, scheduling, and optimization for latency and energy-aware execution.

## Dataset characteristics

- 100 tasks per graph by default
- mix of large and small tasks
- DAG structure with layered dependencies
- resource tier profile: edge, fog, cloud
- CSV outputs for task metadata, graph dependencies, and resource model
- Python-based generator for reproducible dataset creation

## Repository structure

- `scripts/generate_dataset.py` — generator for synthetic task flow graphs
- `data/generated/tasks.csv` — synthetic tasks table
- `data/generated/edges.csv` — dependency edges between tasks
- `data/generated/resources.csv` — fog/edge/cloud node configuration
- `README.md` — project documentation

## Quick start

1. Clone the repository
2. Install Python dependencies if needed
3. Run the generator:

```bash
python scripts/generate_dataset.py --num-tasks 100 --num-graphs 5 --output-dir data/generated
```

This creates CSV files in the output directory.

## Output schema

### `tasks.csv`

Columns:

- `graph_id`
- `task_id`
- `task_type` (`small` or `large`)
- `layer`
- `compute_cost_edge`
- `compute_cost_fog`
- `compute_cost_cloud`
- `memory_mb`
- `preferred_resource`
- `deadline_ms`

### `edges.csv`

Columns:

- `graph_id`
- `src_task_id`
- `dst_task_id`
- `communication_cost`
- `bandwidth_mb_per_s`

### `resources.csv`

Columns:

- `resource_id`
- `resource_type`
- `location`
- `capacity_mips`
- `latency_ms`
- `energy_per_second`

## Example usage

A latency- or energy-aware task allocation framework can load the generated data and then:

- map each task to an available edge/fog/cloud resource
- minimize end-to-end latency
- respect task deadlines and communication dependencies
- consider energy profiles of each tier

## Notes

The generator is deliberately synthetic and can be adapted to match your target environment. If you are testing an optimization algorithm, you can vary:

- number of tasks
- number of graphs
- task-size skew
- communication density
- resource heterogeneity
- deadline constraints

## License

MIT
