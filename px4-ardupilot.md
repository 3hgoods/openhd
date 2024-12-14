

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

ardupilot와 PX4 변수 비교 표 작성해 줘
ChatGPT said:
ChatGPT
ArduPilot과 PX4는 둘 다 오픈 소스 비행 제어 소프트웨어로, 각 시스템에서 사용하는 파라미터가 비슷한 목적을 가지고 있지만 이름과 세부 설정이 다를 수 있습니다. 아래는 ArduPilot과 PX4의 주요 파라미터들을 비교한 표입니다.

기능	                ArduPilot 변수	                PX4 변수	        설명
최대 가속도 (수평)	ATC_ACCEL_MAX	                ATC_ACCEL_X_MAX, ATC_ACCEL_Y_MAX	수평 비행에서 최대 가속도를 설정합니다.
최대 기울기	ATC_ANG_RLL_MAX, ATC_ANG_PIT_MAX	MPC_XY_CRUISE_MAX	비행체의 최대 기울기 각도를 설정합니다.
롤, 피치 비율 제한	ATC_RAT_RLL_P, ATC_RAT_PIT_P	MPC_THR_HOVER	롤과 피치의 비율을 제어하는 비율 설정 값입니다.
롤, 피치 PID 게인	ATC_RAT_RLL_P, ATC_RAT_PIT_P	MC_ROLL_P, MC_PITCH_P	롤과 피치의 PID 컨트롤러 파라미터입니다.
고도 유지 PID	ALT_HOLD_P	MPC_ALT_P	고도를 유지하는 PID 제어 파라미터입니다.
이륙 고도	RTL_ALT	NAV_RTL_ALT	이륙 시 설정할 고도를 지정하는 파라미터입니다.
수평 속도 제한	NAV_SPEED	MPC_XY_VEL_MAX	비행체의 최대 수평 속도를 설정합니다.
수직 속도 제한	NAV_VEL	MPC_Z_VEL_MAX	비행체의 최대 수직 속도를 설정합니다.
이륙 고도 제한	THR_MIN	MPC_THR_MIN	최소 이륙 고도를 설정합니다.
GPS 위치 정확도	GPS_MAX_ELEVATION	EKF2_GPS_TYPE	GPS 위치의 정확도를 제어하는 파라미터입니다.
최대 회전 속도	ATC_RAT_RLL_VEL_MAX	MPC_TURN_MAX_G	비행체의 최대 회전 속도를 설정합니다.
바람 보정	WIND_SPD	EKF2_WIND	바람 보정 관련 설정을 다루는 변수입니다.
전방 비행 속도 제한	FLIGHT_SPEED	MPC_LAND_SPEED	전방 비행 속도를 제한하는 파라미터입니다.
고정밀 모드	LOITER_RADIUS	MPC_LOITER_RAD	고정밀 비행 (로이터 모드)에서의 비행 반경을 설정합니다.
참




