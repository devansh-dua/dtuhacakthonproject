# SustainSoul Badges System Documentation

## Overview
The SustainSoul badges system is a comprehensive reward mechanism featuring 4 badge categories that motivate users to maintain eco-friendly habits and engage with the community.

---

## 🏆 Badge Categories

### 1. **Progress Badges** (Main Identity)
Based on cumulative Eco Score

| Badge | Score Range | Icon | Description |
|-------|-------------|------|-------------|
| **Eco Starter** | 0–100 | 🌱 | Your eco-friendly journey begins |
| **Eco Builder** | 100–300 | 🌿 | Building sustainable habits |
| **Eco Warrior** | 300–700 | 🌳 | Fighting for the environment |
| **Eco Champion** | 700+ | ♻️ | Maximum eco-impact achieved |

**How it works:** Each blog/activity has a score. Total scores determine which badge you display.

---

### 2. **Streak Badges** (Habit Builder)
Based on daily consistency - Only ONE active at a time

| Badge | Requirement | Icon | Description |
|-------|------------|------|-------------|
| **Bronze Streak** | 3-day consistency | 🥉 | Keep it going! |
| **Silver Streak** | 7-day consistency | 🥈 | Week warrior! |
| **Gold Streak** | 14+ day consistency | 🥇 | Unstoppable! |

**How it works:** Every time you add a blog/activity on a new day, your streak increases. Missing a day resets it to 1.

---

### 3. **Campaign Badges** (Engagement)
Special limited-time challenges - rewards for specific campaigns

| Badge | Requirements | Icon |
|-------|-------------|------|
| **Plastic-Free Week** | Complete the challenge | 🚫🛍️ |
| **Transport Challenge Winner** | Win eco-transport competition | 🚴 |
| **Carbon Neutral Champion** | 14-day carbon-neutral lifestyle | 🌍 |

**How it works:** Enable these when special campaigns/challenges are active.

```javascript
// Example: In your challenge completion handler
import { completeCampaignChallenge } from '../utils/badgeUtils';

completeCampaignChallenge(badgesContext, 'campaign_plastic_free', () => {
  showNotification('🎉 Badge Earned: Plastic-Free Week Completed!');
});
```

---

### 4. **Community Badges** (Engagement)
Based on community interactions

| Badge | Requirement | Icon |
|-------|------------|------|
| **First Helper** | Help 1 person | 🤝 |
| **Community Contributor** | Help 5+ people | 👥 |
| **Eco Ambassador** | Help 10+ people + 5+ posts | 🌟 |

**How it works:** Track interactions on the Community page.

---

## 📂 File Structure

```
src/
├── context/
│   └── BadgesContext.jsx          # Badge logic & state management
├── components/
│   └── Badges.jsx                 # Badge display component
├── styles/
│   └── Badges.css                 # Badge styling
├── utils/
│   └── badgeUtils.js              # Helper functions for badge integration
└── pages/
    └── Myprofile.jsx              # Profile page (displays badges)
```

---

## 🔧 Integration Guide

### Step 1: Access Badge Context
```javascript
import { useContext } from 'react';
import { BadgesContext } from '../context/BadgesContext';

function MyComponent() {
  const badgesContext = useContext(BadgesContext);
  // Now you can use: badgesContext.updateStreak(), etc.
}
```

### Step 2: Common Operations

#### Update Streak (when user creates blog)
```javascript
import { handleActivityCompletion } from '../utils/badgeUtils';

const addBlog = () => {
  // ... add blog logic ...
  const badges = handleActivityCompletion(badgesContext, totalScore);
  console.log('New badge:', badges.progressBadge.name);
};
```

#### Complete a Campaign
```javascript
import { completeCampaignChallenge } from '../utils/badgeUtils';

const finishChallenge = () => {
  completeCampaignChallenge(badgesContext, 'campaign_plastic_free', () => {
    alert('🎉 Challenge Completed!');
  });
};
```

#### Track Community Help
```javascript
import { logCommunityInteraction } from '../utils/badgeUtils';

const helpCommunityMember = () => {
  // ... help logic ...
  logCommunityInteraction(badgesContext, 'help');
};
```

#### Show Progress to Next Badge
```javascript
import { getNextBadgeMilestone } from '../utils/badgeUtils';

const milestone = getNextBadgeMilestone(totalScore);
console.log(`${milestone.pointsNeeded} points to ${milestone.badge.name}`);
console.log(`Progress: ${milestone.percentProgress.toFixed(0)}%`);
```

---

## 🎨 Customizing Badges

### Edit BadgesContext.jsx to:
- Change score requirements
- Add new badges
- Adjust streak day requirements
- Modify badge colors and icons

Example:
```javascript
// In BadgesContext.jsx - BADGES object
CUSTOM_BADGE: {
  ECO_HERO: {
    id: 'eco_hero',
    name: 'Eco Hero',
    description: 'Your custom achievement',
    icon: '🦸',
    color: 'bg-red-100',
    textColor: 'text-red-700',
    borderColor: 'border-red-300',
  }
}
```

---

## 📊 Data Stored in userBadges

```javascript
{
  unlockedBadges: [],           // Array of earned badge IDs
  streakDays: 0,                 // Current streak count
  lastActivityDate: Date,        // Last time user added content
  communityHelps: 0,             // Total times helped others
  completedCampaigns: []         // Array of completed campaign IDs
}
```

---

## 🎯 Best Practices

1. **Call updateStreak()** whenever user creates/uploads content
2. **Celebrate milestones** with notifications/modals
3. **Show progress bars** to encourage users toward next badge
4. **Reset streak properly** after checking 24-hour gap
5. **Test extensively** - Use browser DevTools to check badgesContext state

---

## 🚀 Future Enhancements

- [ ] Leaderboards showing top badge collectors
- [ ] Badge sharing on social media
- [ ] Special seasonal badges
- [ ] Badge trading/gifting system
- [ ] Real-time achievement notifications
- [ ] Mobile push notifications for near-milestone

---

## 📝 Notes

- Badges persist in component state (use localStorage/backend for persistence)
- Progress to max badge is always incentivized
- Streak resets after 1 missed day (customizable)
- Multiple campaign badges can be earned simultaneously

For questions or customization needs, modify `BadgesContext.jsx` or `badgeUtils.js` directly.
