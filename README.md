04.02 화면 설계를 마친 앱 초기버전 a1.0 클론 업로드
04.02 a1.0 설계를 토대로 API와 Navigation 기능 추가 -> a1.1

-a1.1 업데이트 항목[04.02]
hooks       -   useKakaoLogin.ts 추가
api         -   authAPI.ts 추가
Navigation  -   AppNavigator.tsx 추가

LoginScreen 업데이트
- 상단 훅 import 추가
- 카카오버튼 작동방식 변경
import { useKakaoLogin } from '../hooks/useKakaoLogin'; 
 <KakaoButton onPress={handleKakaoLogin} />            
 
APP.tsx 업데이트
-네비게이션 추가로 전체적인 구조 변경
import { NavigationContainer } from '@react-navigation/native';
import AppNavigator from './src/navigation/AppNavigator';
import LoginScreen from './src/screens/LoginScreen';
import ProfileSetupScreen from './src/screens/ProfileSetupScreen';

export default function App() {
  return (
    <NavigationContainer>
      <AppNavigator />
    </NavigationContainer>
  );
}

04.05 프로필 화면 설계 a1.2
RegionSelectionScreen.tsx
-BackHeader가 TypeScrpits 에서 지정받아야하는 Prop을 받지 못하던 문제 해결
-onBack={() => navigation.goBack()}/> 추가

-ProfileSetupScreen 에서 arrowRight 를 누르면 RegionSelectionScreen 으로 이동하는 네비게이션 추가

-RegionSelectionScreen에서 지역을 선택하지 않아도 이동이 가능했던 버그 픽스
-if (!selectedRegions[0]) {
    Alert.alert('지역 선택', '관심 지역을 선택해주세요.');
    return;

-RegionSelectionScreen에서 지역을 선택하고 돌아올경우 선택한 지역 표시 기능 추가
-RegionSelectionScreen에서 지역을 선택하고 돌아오면, 닉네임을 비롯한 모든 정보들이 초기화 되는 버그 픽스
useEffect(() => {
  const { location, nickname, userType, selectedCakes } = route.params || {};
  if (location) setLocation(location);
  if (nickname) setNickname(nickname);
  if (userType !== undefined) setUserType(userType);
  if (selectedCakes) setSelectedCakes(selectedCakes);
}, [route.params]);

