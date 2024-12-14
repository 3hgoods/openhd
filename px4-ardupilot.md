

https://discuss.ardupilot.org/t/initial-parameters-calculator-plugin/56909


        // Do calculations
        static void calc_values()
        {

            atc_accel_y_max = Math.Round((-900 * prop_size + 36000) / 100, 0) * 100;
            acro_yaw_p = 0.5 * atc_accel_y_max / 4500;

            atc_accel_p_max = Math.Round((-81718 * Math.Log(prop_size) + 296856) / 100, 0) * 100;
            atc_accel_r_max = atc_accel_p_max;

            ins_gyro_filter = Math.Round((289.22 * Math.Pow(prop_size, -0.838)), 0);

            atc_rat_pit_fltd = ins_gyro_filter / 2;
            atc_rat_pit_flte = 0;
            atc_rat_pit_fltt = ins_gyro_filter / 2;
            atc_rat_rll_fltd = ins_gyro_filter / 2;
            atc_rat_rll_flte = 0;
            atc_rat_rll_fltt = ins_gyro_filter / 2;
            atc_rat_yaw_fltd = 0;
            atc_rat_yaw_flte = 2;
            atc_rat_yaw_fltt = ins_gyro_filter / 2;

            atc_thr_mix_man = 0.1;
            ins_accel_filter = 20;
            mot_thst_expo = Math.Round(0.1405 * Math.Log(prop_size) + 0.3254, 2);
            mot_thst_hover = 0.2;

            batt_arm_volt = (batt_cells - 1) * 0.1 + 3.6 * batt_cells;
            batt_crt_volt = (batt_cell_min_voltage + 0.2) * batt_cells;
            batt_low_volt = (batt_cell_min_voltage + 0.3) * batt_cells;
            mot_bat_volt_max = batt_cell_max_voltage * batt_cells;
            mot_bat_volt_min = batt_cell_min_voltage * batt_cells;

        }


atc_accel_y_max




