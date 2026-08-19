# Integrated Production and Distribution Planning in Multi-plant Steel Enterprises

## Experimental data and computational results

This repository contains anonymized parameter ranges and computational results supporting the paper **“The Production and Distribution Planning Problem in Multi-Plant Steel Enterprises: Mathematical Model and Fix-and-Optimize Matheuristic.”**

## Repository structure

The repository is organized into twomain directories. The `data` directory describes the key parameter ranges of the test instances, the `results` directory contains the computational evidence reported in the paper.

```text
paper_shared_data/
|-- README.md
|-- README_zh-CN.md
|-- data/
|   `-- instance_parameter_ranges.xlsx
|-- results/
|   |-- 01_algorithm_components.xlsx
|   |-- 02_1_adopted_algorithm_parameters.xlsx
|   |-- 02_2_product_decomposition_tuning.xlsx
|   |-- 02_3_period_decomposition_tuning.xlsx
|   |-- 02_4_dc_decomposition_tuning.xlsx
|   |-- 02_5_initial_solution_accuracy_tuning.xlsx
|   |-- 02_6_dynamic_accuracy_strategy_tuning.xlsx
|   |-- 03_small_scale_computational_results.xlsx
|   |-- 04_large_scale_computational_results.xlsx
|   |-- 05_collaboration_effects.xlsx
|   |-- 06_supplier_capacity_sensitivity.xlsx
|   `-- 07_procurement_price_sensitivity.xlsx
```

## File-to-paper mapping

The table below gives the role of each file and identifies the paper section, table, or figure that it supports. 

| File                                                 | Content                                                                          | Paper location                                        |
| ---------------------------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `data/instance_parameter_ranges.xlsx`                | Instance sizes, pooled parameter ranges, and public generation rules             | Section 6, test-instance description                  |
| `results/01_algorithm_components.xlsx`               | Complete algorithm and four ablated variants, all 10 small instances             | Section 6.1, Table 2                                  |
| `results/02_1_adopted_algorithm_parameters.xlsx`     | Adopted parameter settings used in the main computational experiments            | Section 6.2; Supplementary Material Part B, Table B.1 |
| `results/02_2_product_decomposition_tuning.xlsx`     | Tuning results for the number of products in each product-oriented subproblem    | Section 6.2; Supplementary Material Part B, Table B.2 |
| `results/02_3_period_decomposition_tuning.xlsx`      | Tuning results for the number of periods in each period subset                   | Section 6.2; Supplementary Material Part B, Table B.3 |
| `results/02_4_dc_decomposition_tuning.xlsx`          | Tuning results for the number of DCs in each DC-oriented subproblem              | Section 6.2; Supplementary Material Part B, Table B.4 |
| `results/02_5_initial_solution_accuracy_tuning.xlsx` | Tuning results for the initial MIP gap and subproblem time limit                 | Section 6.2; Supplementary Material Part B, Table B.5 |
| `results/02_6_dynamic_accuracy_strategy_tuning.xlsx` | Fixed versus dynamically tightened subproblem-accuracy settings                  | Section 6.2; Supplementary Material Part B, Table B.6 |
| `results/03_small_scale_computational_results.xlsx`  | F&O, modified Wang et al. (2024), Gurobi incumbents and upper bounds             | Section 6.3, Table 3                                  |
| `results/04_large_scale_computational_results.xlsx`  | F&O, modified Wang et al. (2024), and three heuristic rules                      | Section 6.4, Table 4                                  |
| `results/05_collaboration_effects.xlsx`              | No inter-plant versus full inter-plant semi-finished supply                      | Section 6.5, Figure 4                                 |
| `results/06_supplier_capacity_sensitivity.xlsx`      | Capacity multipliers 0.5x, 1.0x, and 2.0x under both reported scenarios          | Section 6.5, Figure 5(a)                              |
| `results/07_procurement_price_sensitivity.xlsx`      | procurement-price multipliers 0.5x, 1.0x, and 2.0x under both reported scenarios | Section 6.5, Figure 5(b)                              |

## Column definitions

The following text explains the meanings of each column in each file.

### `data/instance_parameter_ranges.xlsx`

Considering that the specific information of the examples may involve the confidential information of the enterprises, this file provides an overview of the approximate scale of the 20 instances used, and gives the key parameter value ranges for 10 of the smaller-scale instances.

The file contains two sheets. Start with `instance_scale` to understand the dimensions of each test instance, then consult `parameter_ranges` for thekey parameter value ranges. The two main data sheets are interpreted as follows.

`instance_scale`:

- `instance_group`: instance size (`small` or `large`).
- `instance`: instance number used in the paper.
- `products`: number of finished products.
- `distribution_centers`: number of distribution centers (DCs).
- `orders`: number of customer orders.
- `plants`: number of production plants.
- `suppliers`: number of external semi-finished-product suppliers.
- `planning_periods`: number of weekly periods.

`parameter_ranges`:

- `parameter_code`: parameter name.

- `description`: parameter definition.

- `pooled_min`, `pooled_max`: smallest and largest generated values pooled across all 10 small-scale instances.

- `unit`: physical or monetary unit.

- `disclosure_note`: scope and confidentiality limitation.

### `results/01_algorithm_components.xlsx`

This file corresponds to the results of Section 6.1. It examines the contribution of each major component of the proposed F&O algorithm. It compares the complete algorithm with four ablated variants on the same 10 small-scale instances.

`instance_results`:

- `Algorithm`: Different algorithm versions in Table 2 (`Complete`, `No-Post`, `No-Product`, `No-Period`, or `No-DC`).
- `instance`: small-instance number.
- `solve_time_s`: solution time in seconds.
- `objective_CNY`: objective of the solution.

`summary` averages solution time and objective over all 10 instances for each algorithm version. 

### `results/02_1_adopted_algorithm_parameters.xlsx`

This file corresponds to the adopted algorithm configuration reported in Section 6.2 and Table B.1 of the Supplementary Material. It summarizes the parameter settings used in the main computational experiments after the tuning analyses.

This file contains one sheet, `adopted_parameters`, and the meanings of each column are as follows.

- `stage`: algorithm phase or decomposition strategy.
- `parameter`: parameter name.
- `value`: adopted parameter value.
- `unit`: products, periods, DCs, seconds, iterations, or a fractional MIP gap.

### `results/02_2_product_decomposition_tuning.xlsx`

This file corresponds to the product-oriented decomposition parameter tuning in Section 6.2 and Table B.2 of the Supplementary Material. It compares different numbers of products included in each subproblem on the same 10 small-scale instances.

This file contains two sheets. `product_detail` presents the result for every instance and candidate setting, while `product_summary` reports the average result across the 10 instances for each setting.

- `products_per_subproblem`: number of products included in each product-oriented subproblem.
- `instance`: small-instance number.
- `solve_time_s`: solution time in seconds.
- `objective_CNY`: objective of the solution.
- `average_solve_time_s`, `average_objective_CNY`: averages reported in `product_summary`.

### `results/02_3_period_decomposition_tuning.xlsx`

This file corresponds to the period-oriented decomposition parameter tuning in Section 6.2 and Table B.3 of the Supplementary Material. It compares different numbers of planning periods in each subset while recording the associated product-subproblem size.

This file contains two sheets. `period_detail` presents the result for every instance and candidate setting, while `period_summary` reports the average result across the 10 instances for each setting.

- `periods_per_subset`: number of planning periods included in each period subset.
- `products_per_subproblem`: number of products included in the associated subproblem; this supporting setting is recorded in `period_detail` only.
- `instance`: small-instance number.
- `solve_time_s`: solution time in seconds.
- `objective_CNY`: objective of the solution.
- `average_solve_time_s`, `average_objective_CNY`: averages reported in `period_summary`.

### `results/02_4_dc_decomposition_tuning.xlsx`

This file corresponds to the DC-oriented decomposition parameter tuning in Section 6.2 and Table B.4 of the Supplementary Material. It compares different numbers of distribution centers included in each DC-oriented subproblem.

This file contains two sheets. `dc_detail` presents the result for every instance and candidate setting, while `dc_summary` reports the average result across the 10 instances for each setting.

- `DCs_per_subproblem`: number of DCs included in each DC-oriented subproblem.
- `instance`: small-instance number.
- `solve_time_s`: solution time in seconds.
- `objective_CNY`: objective of the solution.
- `published_DCs_per_subproblem`, `average_solve_time_s`, `average_objective_CNY`: the same candidate DC setting shown as `DCs_per_subproblem` in `dc_detail`, followed by its averages in `dc_summary`.

### `results/02_5_initial_solution_accuracy_tuning.xlsx`

This file corresponds to the initial-solution accuracy parameter tuning in Section 6.2 and Table B.5 of the Supplementary Material. It compares combinations of the initial MIP gap and subproblem time limit on the same 10 small-scale instances.

This file contains two sheets. `accuracy_detail` presents the result for every instance and parameter combination, while `accuracy_summary` reports the average result across the 10 instances for each combination.

- `initial_MIP_gap`: MIP optimality gap used for the initial subproblems.
- `initial_time_limit_s`: time limit for each initial subproblem in seconds.
- `instance`: small-instance number.
- `solve_time_s`: solution time in seconds.
- `objective_CNY`: objective of the solution.
- `average_solve_time_s`, `average_objective_CNY`: averages reported in `accuracy_summary`.

### `results/02_6_dynamic_accuracy_strategy_tuning.xlsx`

This file corresponds to the subproblem-accuracy strategy comparison in Section 6.2 and Table B.6 of the Supplementary Material. It compares fixed optimality gaps and solution times with a strategy that dynamically tightens both settings during the algorithm.

This file contains two sheets. `dynamic_detail` presents the result for every instance and strategy, while `dynamic_summary` reports the average result across the 10 instances for each strategy.

- `Algorithm setting`: fixed or dynamically tightened optimality gaps and solution time.
- `instance`: small-instance number.
- `solve_time_s`: solution time in seconds.
- `objective_CNY`: objective of the solution.
- `accuracy_strategy`, `average_solve_time_s`, `average_objective_CNY`: the same strategy identified by `Algorithm setting` in `dynamic_detail`, followed by its averages in `dynamic_summary`.

### `results/03_small_scale_computational_results.xlsx`

This file corresponds to the results in Table 3 of Section 6.3. It compares F&O with the modified Wang et al. (2024) method and direct Gurobi optimization.

This file contains a sheet, and the meanings of each column are as follows. 

- `instance`, `products`, `DCs`, `orders`: instance indexs and size.
- `FO_time_s`, `FO_objective_CNY`: F&O solution time and net objective.
- `Wang_objective_CNY`: net objective from the modified Wang et al. (2024) comparison method.
- `Gurobi_time_s`, `Gurobi_objective_CNY`: Gurobi wall-clock time and best feasible incumbent.
- `Gurobi_upper_bound_CNY`: upper bound obtained by Gurobi.
- `FO_gap_to_UB`, `Wang_gap_to_UB`, `Gurobi_gap_to_UB`: `(upper bound - method objective) / upper bound`.

The `Average` row reports the average result.

### `results/04_large_scale_computational_results.xlsx`

This file corresponds to the results in Table 4 of Section 6.4. It evaluates scalability on instances closer to the enterprise's operational problem size. F&O is compared with the modified Wang et al. (2024) method and three rule-based heuristics.

This file contains a sheet, and the meanings of each column are as follows.

- `instance`, `products`, `DCs`, `orders`: instance indexsand size.
- `FO_objective_CNY`, `Wang_objective_CNY`: net objective from F&O and the modified Wang et al. (2024) method.
- `SPT_objective_CNY`: result of the shortest-processing-time rule.
- `shortest_distance_objective_CNY`: result of the shortest-distance-first rule.
- `minimum_cost_objective_CNY`: result of the minimum-cost rule.
- `Wang_gap_to_FO`: `(FO_objective_CNY - Wang_objective_CNY) / FO_objective_CNY`.
- `best_rule_gap_to_FO`: relative gap between F&O and the best of the three heuristic-rule objectives.

`The `Average` row reports the average result.

### `results/05_collaboration_effects.xlsx`

This file corresponds to the result of Figure 4 in Section 6.5. It quantifies the effect of allowing semi-finished products to supply between plants. Each small-scale instance is solved under identical parameter data in two scenarios：no inter-plant supply and full inter-plant supply.

This file contains three sheets. `instance_results` presents various metrics for different instances under each scenario, while `scenario_averages` shows the averaged results across all instances for each scenario. `reported_changes` reports the percentage variations of the metrics in Figure 4 for the `no inter-plant` scenario relative to the `full inter-plant` scenario. The definitions of each column in these sheets are provided below.

- `instance`: instance index.

- `scenario`:  scenario types (`no_interplant` or `full_interplant`).

- `total_profit_CNY`: sales revenue minus all modeled costs.

- `sales_revenue_CNY`: revenue from delivered finished products.

- `external_procurement_cost_CNY`: cost of externalprocurementased semi-finished products.

- `external_procurement_quantity_t`: externprocurementase quantity in tons.

- `transport_cost_CNY`: transportation cost.

In `scenario_averages`, the five outcome columns are prefixed with `average_` and report the mean across the 10 instances for each scenario. `reported_changes` calculates `(full inter-plant - no inter-plant) / no inter-plant` for the four Figure 4 metrics.

### `results/06_supplier_capacity_sensitivity.xlsx`

This file corresponds to the result of Figure 5(a) in Section 6.5. It examines the effect of external supplier capacity on inter-plant collaboration by testing tight, base, and abundant supplier-capacity settings under both collaboration scenarios.

This file contains two sheets. `instance_results` presents the metrics for every instance, supplier-capacity setting, and collaboration scenario, while `scenario_averages` reports the averaged results across all 10 instances for each setting and scenario. The meanings of the columns in these sheets are provided below.

- `instance`: instance index.
- `supplier_capacity`: supplier-capacity setting (`tight`, `base`, or `abundant`), corresponding to 0.5x, 1.0x, or 2.0x the base capacity.
- `scenario`: scenario type (`no_interplant` or `full_interplant`).
- `total_profit_CNY`: sales revenue minus all modeled costs.
- `sales_revenue_CNY`: revenue from delivered finished products.
- `external_procurement_cost_CNY`: cost of externally procured semi-finished products.
- `external_procurement_quantity_t`: external procurement quantity in tons.
- `transport_cost_CNY`: transportation cost.

In `scenario_averages`, the five outcome columns are prefixed with `average_` and report the mean across the 10 instances for each supplier-capacity and scenario combination.

### `results/07_procurement_price_sensitivity.xlsx`

This file corresponds to the result of Figure 5(b) in Section 6.5. It examines the effect of external procurement prices on inter-plant collaboration by testing low, base, and high procurement-price settings under both collaboration scenarios.

This file contains two sheets. `instance_results` presents the metrics for every instance, procurement-price setting, and collaboration scenario, while `scenario_averages` reports the averaged results across all 10 instances for each setting and scenario. The meanings of the columns in these sheets are provided below.

- `instance`: instance index.
- `procurement_price`: procurement-price setting (`low`, `base`, or `high`), corresponding to 0.5x, 1.0x, or 2.0x the base price.
- `scenario`: scenario type (`no_interplant` or `full_interplant`).
- `total_profit_CNY`: sales revenue minus all modeled costs.
- `sales_revenue_CNY`: revenue from delivered finished products.
- `external_procurement_cost_CNY`: cost of externally procured semi-finished products.
- `external_procurement_quantity_t`: external procurement quantity in tons.
- `transport_cost_CNY`: transportation cost.

In `scenario_averages`, the five outcome columns are prefixed with `average_` and report the mean across the 10 instances for each procurement-price and scenario combination.
