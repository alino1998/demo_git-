import {
  createStackNavigator,
  createAppContainer,
  createDrawerNavigator,
} from 'react-navigation';
import Home from '../components/Home';
import HistoEnCours from '../components/HistoEnCours';
import Page2 from '../components/Page2';
import Page3 from '../components/Page3';
import { Foundation, FontAwesome } from '@expo/vector-icons';
import * as React from 'react';
import {
  Text,
  View,
  StyleSheet,
  TouchableOpacity,
  Button,
  Animated,
} from 'react-native';

const styles = StyleSheet.create({
  styleDrawingIcone: {
    marginLeft: 20,
  },
  stylePhotoUser: {
    height: 150,
    flex: 1,
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
  },
});
class AfficherDrawer extends React.Component {
  constructor(props) {
    super(props);
  }

  executeur = () => {
    this.props.pa();
  };

  render() {
    return (
      <TouchableOpacity
        onPress={() => this.executeur()}
        style={styles.styleDrawingIcone}>
        <Foundation name="list" size={32} color="white" />
      </TouchableOpacity>
    );
  }
}
class AfficherProfil extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <View style={styles.stylePhotoUser}>
        <FontAwesome name="user-o" size={70} color="black" />
      </View>
    );
  }
}

const AppNavigator = createStackNavigator(
  {
    Home: {
      screen: Home,
      navigationOptions: function({ navigation }) {
        return {
          headerTitle: 'Home',
          headerLeft: <AfficherDrawer pa={navigation.getParam('open')} />,
        };
      },
    },
    Page2: {
      screen: Page2,
      navigationOptions: {
        headerTitle: 'Page2',
      },
    },
    Page3: {
      screen: Page3,
      navigationOptions: {
        headerTitle: 'Page3',
      },
    },
    Histo: {
      screen: HistoEnCours,
      navigationOptions: {
        headerTitle: 'Historique',
      },
    },
  },
  {
    initialRouteName: 'Home',
    defaultNavigationOptions: {
      headerTintColor: '#ecf0f1',
      headerStyle: {
        backgroundColor: '#d35400',
        height: 60,
      },
      headerTitleStyle: {
        fontSize: 22,
      },
    },
  }
);

const MyDrawerNavigator = createDrawerNavigator(
  {
    O: {
      screen: Home,
      navigationOptions: {
        drawerLabel: <AfficherProfil />,
      },
    },
    Mystack: {
      screen: AppNavigator,
    },
    Yes: {
      screen: AppNavigator,
      navigationOptions: {
        drawerLabel: 'Historique',
        // drawerIcon: () => <Foundation name="list" size={32} color="white" />,
      },
    },
  },
  {
    initialRouteName: 'Mystack',
    drawerBackgroundColor: 'white',
    drawerPosition: 'left',
    drawerWidth: 300,
    contentOptions: {
      activeBackgroundColor: '#d35400',
    },
  }
);
const Second = createStackNavigator(
  {
    Z1: {
      screen: 'Home',
    },
    Z2: {
      screen: 'HistoEnCours',
    },
  },
  {
    initialRouteName: 'Z2',
  }
);
const MyApp = createAppContainer(MyDrawerNavigator);
export default MyApp;
