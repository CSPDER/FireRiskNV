# FireRiskNV
// FireSafetyDashboard.tsx
import React from 'react';
import { Grid, Typography, Paper } from '@mui/material';
import LocationPanel from './components/LocationPanel';
import WeatherPanel from './components/WeatherPanel';
import FireDangerPanel from './components/FireDangerPanel';
import JurisdictionPanel from './components/JurisdictionPanel';
import EquipmentPanel from './components/EquipmentPanel';
import StrategyPanel from './components/StrategyPanel';

const FireSafetyDashboard: React.FC = () => {
  return (
    <Grid container spacing={3} padding={2}>
      <Grid item xs={12}>
        <Typography variant="h4">🔥 NV Energy Fire Safety Strategy</Typography>
      </Grid>

      <Grid item xs={12} md={6}>
        <LocationPanel />
        <WeatherPanel />
        <FireDangerPanel />
      </Grid>

      <Grid item xs={12} md={6}>
        <JurisdictionPanel />
        <EquipmentPanel />
        <StrategyPanel />
      </Grid>
    </Grid>
  );
};

export default FireSafetyDashboard;// StrategyPanel.tsx
import React from 'react';
import { Paper, Typography, List, ListItem } from '@mui/material';
import { useFireContext } from '../context/FireContext';

const StrategyPanel: React.FC = () => {
  const { location, weather, fireDanger, heatIndex, aqi, jurisdiction, blmStip5, usfsPAL, equipment, ndpp } = useFireContext();

  const generateStrategy = () => {
    const actions: string[] = [];

    if (fireDanger === 'Extreme' || usfsPAL >= 4) {
      actions.push('Initiate PSOM protocols');
      actions.push('Suspend non-essential field operations');
    }

    if (heatIndex > 100 || aqi > 150) {
      actions.push('Limit crew exposure; rotate shifts');
    }

    if (blmStip5 === 'Strict Liability') {
      actions.push('Document all mitigation steps; notify BLM contact');
    }

    if (ndpp.includes('De-energization')) {
      actions.push('Review NDPP de-energization zones');
    }

    return actions;
  };

  return (
    <Paper elevation={3} sx={{ padding: 2 }}>
      <Typography variant="h6">Recommended Actions</Typography>
      <List>
        {generateStrategy().map((action, index) => (
          <ListItem key={index}>✅ {action}</ListItem>
        ))}
      </List>
    </Paper>
  );
};

export default StrategyPanel;


