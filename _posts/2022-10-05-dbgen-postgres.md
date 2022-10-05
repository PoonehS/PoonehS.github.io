# A pitfall generating the data from postgres TPC-H dbgen
I found the script in the `tpch_prepare`, which make the dbgen in parallel. I think it's caused by the PCIe 3.0's bandwidth slowed down some of the other dbgen when running in parallel. So I run them sequencially resolve the problem.
```bash
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T c &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T s &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T n &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T r &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T O &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T L &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T P &
  sudo -u $PGUSER "$BASEDIR/dbgen/dbgen" -s $SCALE -f -v -T S &
```