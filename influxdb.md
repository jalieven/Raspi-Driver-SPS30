CREATE USER admin WITH PASSWORD 'pswd' WITH ALL PRIVILEGES

SHOW FIELD KEYS ON "metrics" FROM "PM1"

CREATE RETENTION POLICY "a_year" ON "metrics" DURATION 52w REPLICATION 1

CREATE CONTINUOUS QUERY "pm0.5_cq_5m" ON "metrics" BEGIN SELECT mean("count_cubic_centimeter") AS "count_cubic_centimeter" INTO "a_year"."PM0.5_5m_downsampled" FROM "PM0.5" GROUP BY time(5m) END

CREATE CONTINUOUS QUERY "pm1_cq_5m" ON "metrics" BEGIN SELECT mean("count_cubic_centimeter") AS "count_cubic_centimeter", mean("microgram_cubic_meter") AS "microgram_cubic_meter" INTO "a_year"."PM1_5m_downsampled" FROM "PM1" GROUP BY time(5m) END

CREATE CONTINUOUS QUERY "pm2.5_cq_5m" ON "metrics" BEGIN SELECT mean("count_cubic_centimeter") AS "count_cubic_centimeter", mean("microgram_cubic_meter") AS "microgram_cubic_meter" INTO "a_year"."PM2.5_5m_downsampled" FROM "PM2.5" GROUP BY time(5m) END

CREATE CONTINUOUS QUERY "pm4_cq_5m" ON "metrics" BEGIN SELECT mean("count_cubic_centimeter") AS "count_cubic_centimeter", mean("microgram_cubic_meter") AS "microgram_cubic_meter" INTO "a_year"."PM4_5m_downsampled" FROM "PM4" GROUP BY time(5m) END

CREATE CONTINUOUS QUERY "pm10_cq_5m" ON "metrics" BEGIN SELECT mean("count_cubic_centimeter") AS "count_cubic_centimeter", mean("microgram_cubic_meter") AS "microgram_cubic_meter" INTO "a_year"."PM10_5m_downsampled" FROM "PM10" GROUP BY time(5m) END

CREATE CONTINUOUS QUERY "particle_size_cq_5m" ON "metrics" BEGIN SELECT mean("typical_particle_size") AS "typical_particle_size" INTO "a_year"."Particles_5m_downsampled" FROM "Particles" GROUP BY time(5m) END

SELECT * FROM "a_year"."PM1_5m_downsampled"

SELECT * FROM "a_year"."Particles_5m_downsampled"