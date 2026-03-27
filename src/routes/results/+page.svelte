<script>
	import { page } from '$app/stores';

	// ---- Parse query params ----
	$: moodsParam = $page.url.searchParams.get('moods') || '';
	$: budget = $page.url.searchParams.get('budget') || '40';
	$: solo = $page.url.searchParams.get('solo') === 'true';
	$: outdoor = $page.url.searchParams.get('outdoor') === 'true';
	$: moodList = moodsParam ? moodsParam.split(',') : [];

	// ---- Restaurant Database ----
	/** @type {Array<{id: string, name: string, cuisine: string, rating: number, reviews: number, priceGel: number, avgCheck: string, distance: string, tags: string[], image: string, moods: string[], menu: Array<{name: string, price: string, image: string}>, address: string, hours: string, outdoor: boolean, soloFriendly: boolean}>} */
	const allRestaurants = [
		{
			id: 'shavi-lomi',
			name: 'Shavi Lomi',
			cuisine: 'Modern Georgian',
			rating: 4.8,
			reviews: 1247,
			priceGel: 35,
			avgCheck: '₾25–45',
			distance: '0.8 km',
			tags: ['Fine Dining', 'Wine Bar', 'Vegetarian Options'],
			image: 'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?w=600&h=400&fit=crop',
			moods: ['chill', 'romantic', 'foodie'],
			menu: [
				{ name: 'Khinkali Truffle', price: '₾18', image: 'https://images.unsplash.com/photo-1625398407796-82650a8c135f?w=300&h=200&fit=crop' },
				{ name: 'Lobio in Ketsi', price: '₾14', image: 'https://images.unsplash.com/photo-1604908176997-125f25cc6f3d?w=300&h=200&fit=crop' },
				{ name: 'Chakapuli Lamb', price: '₾22', image: 'https://images.unsplash.com/photo-1544025162-d76694265947?w=300&h=200&fit=crop' }
			],
			address: '28 Zubalashvili St, Tbilisi',
			hours: '12:00 – 00:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'cafe-stamba',
			name: 'Stamba Café',
			cuisine: 'European Fusion',
			rating: 4.7,
			reviews: 892,
			priceGel: 45,
			avgCheck: '₾35–60',
			distance: '1.2 km',
			tags: ['Trendy', 'Brunch', 'Cocktails'],
			image: 'https://images.unsplash.com/photo-1554118811-1e0d58224f24?w=600&h=400&fit=crop',
			moods: ['foodie', 'party', 'work'],
			menu: [
				{ name: 'Avocado Toast', price: '₾16', image: 'https://images.unsplash.com/photo-1541519227354-08fa5d50c44d?w=300&h=200&fit=crop' },
				{ name: 'Wagyu Burger', price: '₾32', image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=300&h=200&fit=crop' },
				{ name: 'Passion Fruit Cheesecake', price: '₾18', image: 'https://images.unsplash.com/photo-1524351199432-d330df40fdcd?w=300&h=200&fit=crop' }
			],
			address: '14 Merab Kostava St, Tbilisi',
			hours: '08:00 – 01:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'barbarestan',
			name: 'Barbarestan',
			cuisine: 'Heritage Georgian',
			rating: 4.9,
			reviews: 2103,
			priceGel: 55,
			avgCheck: '₾40–70',
			distance: '0.5 km',
			tags: ['Award-Winning', 'Historic', 'Wine Pairing'],
			image: 'https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=600&h=400&fit=crop',
			moods: ['romantic', 'foodie', 'family'],
			menu: [
				{ name: 'Pkhali Trio', price: '₾15', image: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=300&h=200&fit=crop' },
				{ name: 'Duck Tsitsila', price: '₾38', image: 'https://images.unsplash.com/photo-1432139509613-5c4255a1d1f6?w=300&h=200&fit=crop' },
				{ name: 'Churchkhela Dessert', price: '₾12', image: 'https://images.unsplash.com/photo-1551024506-0bccd828d307?w=300&h=200&fit=crop' }
			],
			address: '132 D. Aghmashenebeli Ave, Tbilisi',
			hours: '12:00 – 23:00',
			outdoor: false,
			soloFriendly: false
		},
		{
			id: 'lineville',
			name: 'Lineville',
			cuisine: 'Italian & Georgian',
			rating: 4.6,
			reviews: 634,
			priceGel: 30,
			avgCheck: '₾20–40',
			distance: '1.5 km',
			tags: ['Casual', 'Pizza', 'Family-Friendly'],
			image: 'https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=600&h=400&fit=crop',
			moods: ['family', 'chill', 'work'],
			menu: [
				{ name: 'Margherita Pizza', price: '₾16', image: 'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=300&h=200&fit=crop' },
				{ name: 'Adjarian Khachapuri', price: '₾14', image: 'https://images.unsplash.com/photo-1618403088890-3d9ff6f4c8b1?w=300&h=200&fit=crop' },
				{ name: 'Tiramisu', price: '₾12', image: 'https://images.unsplash.com/photo-1571877227200-a0d98ea607e9?w=300&h=200&fit=crop' }
			],
			address: '5 Shardeni St, Tbilisi',
			hours: '10:00 – 23:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'keto-and-kote',
			name: 'Keto & Kote',
			cuisine: 'Georgian Comfort',
			rating: 4.5,
			reviews: 1456,
			priceGel: 20,
			avgCheck: '₾12–25',
			distance: '0.3 km',
			tags: ['Budget-Friendly', 'Traditional', 'Quick Bites'],
			image: 'https://images.unsplash.com/photo-1466978913421-dad2ebd01d17?w=600&h=400&fit=crop',
			moods: ['chill', 'family', 'work'],
			menu: [
				{ name: 'Khinkali (10 pcs)', price: '₾8', image: 'https://images.unsplash.com/photo-1625398407796-82650a8c135f?w=300&h=200&fit=crop' },
				{ name: 'Ojakhuri', price: '₾14', image: 'https://images.unsplash.com/photo-1504674900247-0877df9cc836?w=300&h=200&fit=crop' },
				{ name: 'Mtsvadi Skewers', price: '₾16', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=300&h=200&fit=crop' }
			],
			address: '3 Bambis Rigi, Tbilisi',
			hours: '09:00 – 22:00',
			outdoor: false,
			soloFriendly: true
		},
		{
			id: 'rooms-hotel',
			name: 'Rooms Hotel Restaurant',
			cuisine: 'Contemporary European',
			rating: 4.7,
			reviews: 978,
			priceGel: 60,
			avgCheck: '₾45–80',
			distance: '1.8 km',
			tags: ['Upscale', 'Cocktail Bar', 'Terrace'],
			image: 'https://images.unsplash.com/photo-1559339352-11d035aa65de?w=600&h=400&fit=crop',
			moods: ['romantic', 'party', 'foodie'],
			menu: [
				{ name: 'Beef Tartare', price: '₾28', image: 'https://images.unsplash.com/photo-1625937286520-3ef7a0ea7763?w=300&h=200&fit=crop' },
				{ name: 'Sea Bass Fillet', price: '₾36', image: 'https://images.unsplash.com/photo-1519708227418-c8fd9a32b7a2?w=300&h=200&fit=crop' },
				{ name: 'Chocolate Fondant', price: '₾20', image: 'https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=300&h=200&fit=crop' }
			],
			address: '14 Merab Kostava St, Tbilisi',
			hours: '07:00 – 01:00',
			outdoor: true,
			soloFriendly: false
		},
		{
			id: 'vino-underground',
			name: 'Vino Underground',
			cuisine: 'Wine Bar & Tapas',
			rating: 4.6,
			reviews: 523,
			priceGel: 35,
			avgCheck: '₾25–45',
			distance: '0.6 km',
			tags: ['Natural Wine', 'Cozy', 'Late Night'],
			image: 'https://images.unsplash.com/photo-1543007630-9710e4a00a20?w=600&h=400&fit=crop',
			moods: ['chill', 'romantic', 'party'],
			menu: [
				{ name: 'Cheese Board', price: '₾22', image: 'https://images.unsplash.com/photo-1452195100486-9cc805987862?w=300&h=200&fit=crop' },
				{ name: 'Bruschetta Trio', price: '₾16', image: 'https://images.unsplash.com/photo-1572695157366-5e585ab2b69f?w=300&h=200&fit=crop' },
				{ name: 'Qvevri Wine Glass', price: '₾14', image: 'https://images.unsplash.com/photo-1510812431401-41d2bd2722f3?w=300&h=200&fit=crop' }
			],
			address: '15 Galaktion Tabidze St, Tbilisi',
			hours: '15:00 – 02:00',
			outdoor: false,
			soloFriendly: true
		},
		{
			id: 'tsiskvili',
			name: 'Tsiskvili',
			cuisine: 'Traditional Georgian',
			rating: 4.4,
			reviews: 2340,
			priceGel: 25,
			avgCheck: '₾15–30',
			distance: '2.1 km',
			tags: ['Live Music', 'Large Groups', 'Garden'],
			image: 'https://images.unsplash.com/photo-1578474846511-04ba529f0b88?w=600&h=400&fit=crop',
			moods: ['party', 'family', 'chill'],
			menu: [
				{ name: 'Satsivi', price: '₾14', image: 'https://images.unsplash.com/photo-1547592180-85f173990554?w=300&h=200&fit=crop' },
				{ name: 'Kababi', price: '₾18', image: 'https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?w=300&h=200&fit=crop' },
				{ name: 'Badrijani Nigvzit', price: '₾10', image: 'https://images.unsplash.com/photo-1540189549336-e6e99c3679fe?w=300&h=200&fit=crop' }
			],
			address: '1 Lermontov St, Tbilisi',
			hours: '11:00 – 00:00',
			outdoor: true,
			soloFriendly: false
		},
		{
			id: 'sakhachapure-n1',
			name: 'Sakhachapure №1',
			cuisine: 'Georgian Bakery',
			rating: 4.6,
			reviews: 3210,
			priceGel: 12,
			avgCheck: '₾6–15',
			distance: '0.4 km',
			tags: ['Budget-Friendly', 'Quick Service', 'Student Favorite'],
			image: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?w=600&h=400&fit=crop',
			moods: ['chill', 'work', 'family'],
			menu: [
				{ name: 'Imeruli Khachapuri', price: '₾7', image: 'https://images.unsplash.com/photo-1618403088890-3d9ff6f4c8b1?w=300&h=200&fit=crop' },
				{ name: 'Lobiani', price: '₾5', image: 'https://images.unsplash.com/photo-1509440159596-0249088772ff?w=300&h=200&fit=crop' },
				{ name: 'Kubdari', price: '₾9', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=300&h=200&fit=crop' }
			],
			address: '7 Kote Abkhazi St, Tbilisi',
			hours: '08:00 – 22:00',
			outdoor: false,
			soloFriendly: true
		},
		{
			id: 'maspindzelo',
			name: 'Maspindzelo',
			cuisine: 'Traditional Georgian',
			rating: 4.5,
			reviews: 1678,
			priceGel: 22,
			avgCheck: '₾15–28',
			distance: '0.7 km',
			tags: ['Authentic', 'Generous Portions', 'Locals Choice'],
			image: 'https://images.unsplash.com/photo-1592861956120-e524fc739696?w=600&h=400&fit=crop',
			moods: ['family', 'chill', 'foodie'],
			menu: [
				{ name: 'Shkmeruli', price: '₾16', image: 'https://images.unsplash.com/photo-1598103442097-8b74394b95c6?w=300&h=200&fit=crop' },
				{ name: 'Tolma', price: '₾12', image: 'https://images.unsplash.com/photo-1540189549336-e6e99c3679fe?w=300&h=200&fit=crop' },
				{ name: 'Churchkhela Plate', price: '₾8', image: 'https://images.unsplash.com/photo-1551024506-0bccd828d307?w=300&h=200&fit=crop' }
			],
			address: '36 D. Aghmashenebeli Ave, Tbilisi',
			hours: '10:00 – 23:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'ezo',
			name: 'Ezo',
			cuisine: 'Georgian & Mediterranean',
			rating: 4.7,
			reviews: 743,
			priceGel: 40,
			avgCheck: '₾30–50',
			distance: '1.0 km',
			tags: ['Courtyard Dining', 'Date Night', 'Wine List'],
			image: 'https://images.unsplash.com/photo-1600891964599-f61ba0e24092?w=600&h=400&fit=crop',
			moods: ['romantic', 'chill', 'foodie'],
			menu: [
				{ name: 'Grilled Veal Chops', price: '₾34', image: 'https://images.unsplash.com/photo-1544025162-d76694265947?w=300&h=200&fit=crop' },
				{ name: 'Eggplant Rollatini', price: '₾18', image: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=300&h=200&fit=crop' },
				{ name: 'Crème Brûlée', price: '₾14', image: 'https://images.unsplash.com/photo-1470124182917-cc6e71b22ecc?w=300&h=200&fit=crop' }
			],
			address: '2 Abanos St, Old Tbilisi',
			hours: '12:00 – 00:00',
			outdoor: true,
			soloFriendly: false
		},
		{
			id: 'lolita',
			name: 'Lolita',
			cuisine: 'Asian Fusion & Cocktails',
			rating: 4.5,
			reviews: 567,
			priceGel: 38,
			avgCheck: '₾28–48',
			distance: '1.3 km',
			tags: ['Cocktail Bar', 'Late Night', 'DJ Sets'],
			image: 'https://images.unsplash.com/photo-1514933651103-005eec06c04b?w=600&h=400&fit=crop',
			moods: ['party', 'foodie', 'chill'],
			menu: [
				{ name: 'Spicy Tuna Roll', price: '₾22', image: 'https://images.unsplash.com/photo-1579871494447-9811cf80d66c?w=300&h=200&fit=crop' },
				{ name: 'Pad Thai', price: '₾20', image: 'https://images.unsplash.com/photo-1559314809-0d155014e29e?w=300&h=200&fit=crop' },
				{ name: 'Matcha Tiramisu', price: '₾16', image: 'https://images.unsplash.com/photo-1563805042-7684c019e1cb?w=300&h=200&fit=crop' }
			],
			address: '20 Chardin St, Tbilisi',
			hours: '17:00 – 03:00',
			outdoor: false,
			soloFriendly: true
		},
		{
			id: 'khasheria',
			name: 'Khasheria',
			cuisine: 'Traditional Georgian Diner',
			rating: 4.3,
			reviews: 890,
			priceGel: 15,
			avgCheck: '₾8–18',
			distance: '1.6 km',
			tags: ['Ultra Budget', '24/7', 'Late Night Eats'],
			image: 'https://images.unsplash.com/photo-1552566626-52f8b828add9?w=600&h=400&fit=crop',
			moods: ['party', 'chill', 'work'],
			menu: [
				{ name: 'Khashi (Traditional Soup)', price: '₾8', image: 'https://images.unsplash.com/photo-1547592180-85f173990554?w=300&h=200&fit=crop' },
				{ name: 'Khinkali (5 pcs)', price: '₾4', image: 'https://images.unsplash.com/photo-1625398407796-82650a8c135f?w=300&h=200&fit=crop' },
				{ name: 'Mtsvadi + Bread', price: '₾10', image: 'https://images.unsplash.com/photo-1529692236671-f1f6cf9683ba?w=300&h=200&fit=crop' }
			],
			address: '42 Chavchavadze Ave, Tbilisi',
			hours: '00:00 – 23:59',
			outdoor: false,
			soloFriendly: true
		},
		{
			id: 'republic',
			name: 'Republic Grill & Bar',
			cuisine: 'American & Georgian',
			rating: 4.4,
			reviews: 412,
			priceGel: 35,
			avgCheck: '₾25–45',
			distance: '1.1 km',
			tags: ['Sports Bar', 'Burgers', 'Craft Beer'],
			image: 'https://images.unsplash.com/photo-1572116469696-31de0f17cc34?w=600&h=400&fit=crop',
			moods: ['party', 'chill', 'work'],
			menu: [
				{ name: 'Republic Smash Burger', price: '₾22', image: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=300&h=200&fit=crop' },
				{ name: 'BBQ Ribs Half Rack', price: '₾28', image: 'https://images.unsplash.com/photo-1544025162-d76694265947?w=300&h=200&fit=crop' },
				{ name: 'Craft Beer Flight', price: '₾16', image: 'https://images.unsplash.com/photo-1535958636474-b021ee887b13?w=300&h=200&fit=crop' }
			],
			address: '3 Pushkin St, Tbilisi',
			hours: '12:00 – 02:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'pasanauri',
			name: 'Pasanauri',
			cuisine: 'Georgian Chain Restaurant',
			rating: 4.3,
			reviews: 4120,
			priceGel: 18,
			avgCheck: '₾10–22',
			distance: '0.5 km',
			tags: ['Reliable', 'Fast Service', 'Central Location'],
			image: 'https://images.unsplash.com/photo-1586999768265-24af89630739?w=600&h=400&fit=crop',
			moods: ['family', 'work', 'chill'],
			menu: [
				{ name: 'Khinkali Assorted (10)', price: '₾9', image: 'https://images.unsplash.com/photo-1625398407796-82650a8c135f?w=300&h=200&fit=crop' },
				{ name: 'Chicken Tabaka', price: '₾16', image: 'https://images.unsplash.com/photo-1598103442097-8b74394b95c6?w=300&h=200&fit=crop' },
				{ name: 'Adjarian Khachapuri', price: '₾12', image: 'https://images.unsplash.com/photo-1618403088890-3d9ff6f4c8b1?w=300&h=200&fit=crop' }
			],
			address: '34 Rustaveli Ave, Tbilisi',
			hours: '09:00 – 00:00',
			outdoor: false,
			soloFriendly: true
		},
		{
			id: 'culinarium',
			name: 'Culinarium Khasheria',
			cuisine: 'Modern Georgian Bistro',
			rating: 4.6,
			reviews: 389,
			priceGel: 30,
			avgCheck: '₾20–38',
			distance: '1.4 km',
			tags: ['Farm-to-Table', 'Brunch', 'Natural Wine'],
			image: 'https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=600&h=400&fit=crop',
			moods: ['foodie', 'chill', 'work'],
			menu: [
				{ name: 'Eggs Florentine Georgian', price: '₾14', image: 'https://images.unsplash.com/photo-1525351484163-7529414344d8?w=300&h=200&fit=crop' },
				{ name: 'Mushroom Risotto', price: '₾18', image: 'https://images.unsplash.com/photo-1476124369491-e7addf5db371?w=300&h=200&fit=crop' },
				{ name: 'Homemade Lemonade', price: '₾6', image: 'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=300&h=200&fit=crop' }
			],
			address: '12 Petriashvili St, Tbilisi',
			hours: '09:00 – 23:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'samikitno',
			name: 'Samikitno Machakhela',
			cuisine: 'Georgian Traditional',
			rating: 4.2,
			reviews: 5670,
			priceGel: 16,
			avgCheck: '₾8–20',
			distance: '0.2 km',
			tags: ['Most Reviewed', 'Tourist Friendly', 'Huge Menu'],
			image: 'https://images.unsplash.com/photo-1537047902294-62a40c20a6ae?w=600&h=400&fit=crop',
			moods: ['family', 'chill', 'party'],
			menu: [
				{ name: 'Khachapuri Sampler', price: '₾14', image: 'https://images.unsplash.com/photo-1618403088890-3d9ff6f4c8b1?w=300&h=200&fit=crop' },
				{ name: 'Mixed Grill Platter', price: '₾22', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=300&h=200&fit=crop' },
				{ name: 'Kompot Pitcher', price: '₾5', image: 'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=300&h=200&fit=crop' }
			],
			address: '25 Leselidze St, Tbilisi',
			hours: '08:00 – 01:00',
			outdoor: true,
			soloFriendly: true
		},
		{
			id: 'purpur',
			name: 'Purpur',
			cuisine: 'European & Seafood',
			rating: 4.7,
			reviews: 645,
			priceGel: 50,
			avgCheck: '₾38–65',
			distance: '1.7 km',
			tags: ['Rooftop', 'Seafood', 'Sunset Views'],
			image: 'https://images.unsplash.com/photo-1559339352-11d035aa65de?w=600&h=400&fit=crop',
			moods: ['romantic', 'foodie', 'party'],
			menu: [
				{ name: 'Grilled Octopus', price: '₾32', image: 'https://images.unsplash.com/photo-1565557623262-b51c2513a641?w=300&h=200&fit=crop' },
				{ name: 'Salmon Poke Bowl', price: '₾26', image: 'https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=300&h=200&fit=crop' },
				{ name: 'Pannacotta Rose', price: '₾14', image: 'https://images.unsplash.com/photo-1488477181946-6428a0291777?w=300&h=200&fit=crop' }
			],
			address: '1 Erekle II St, Tbilisi',
			hours: '12:00 – 01:00',
			outdoor: true,
			soloFriendly: false
		},
		{
			id: 'g-vino',
			name: 'G.Vino',
			cuisine: 'Georgian Wine Restaurant',
			rating: 4.8,
			reviews: 921,
			priceGel: 45,
			avgCheck: '₾30–55',
			distance: '0.6 km',
			tags: ['Wine Expert', 'Qvevri Wines', 'Intimate'],
			image: 'https://images.unsplash.com/photo-1510812431401-41d2bd2722f3?w=600&h=400&fit=crop',
			moods: ['romantic', 'chill', 'foodie'],
			menu: [
				{ name: 'Wine & Cheese Pairing', price: '₾35', image: 'https://images.unsplash.com/photo-1452195100486-9cc805987862?w=300&h=200&fit=crop' },
				{ name: 'Lamb Chakapuli', price: '₾24', image: 'https://images.unsplash.com/photo-1544025162-d76694265947?w=300&h=200&fit=crop' },
				{ name: 'Walnut & Honey Dessert', price: '₾12', image: 'https://images.unsplash.com/photo-1519676867240-f03562e64571?w=300&h=200&fit=crop' }
			],
			address: '10 Bambis Rigi, Tbilisi',
			hours: '13:00 – 00:00',
			outdoor: false,
			soloFriendly: true
		}
	];

	// ---- Filtering logic ----
	$: budgetNum = parseInt(budget) || 40;

	$: filteredRestaurants = allRestaurants
		.filter(r => {
			// Mood match: at least one selected mood must match
			if (moodList.length > 0 && !r.moods.some(m => moodList.includes(m))) return false;
			// Budget filter: allow restaurants within reasonable range of budget
			if (r.priceGel > budgetNum * 2) return false;
			// Solo filter
			if (solo && !r.soloFriendly) return false;
			// Outdoor filter
			if (outdoor && !r.outdoor) return false;
			return true;
		})
		.sort((a, b) => {
			// Score: mood overlap * 10 + rating
			const aScore = a.moods.filter(m => moodList.includes(m)).length * 10 + a.rating;
			const bScore = b.moods.filter(m => moodList.includes(m)).length * 10 + b.rating;
			return bScore - aScore;
		});

	// ---- Expanded card state ----
	/** @type {Set<string>} */
	let expandedIds = new Set();

	function toggleExpand(/** @type {string} */ id) {
		if (expandedIds.has(id)) {
			expandedIds.delete(id);
		} else {
			expandedIds.add(id);
		}
		expandedIds = expandedIds; // trigger reactivity
	}

	/** @param {number} rating */
	function stars(rating) {
		const full = Math.floor(rating);
		const half = rating % 1 >= 0.5;
		return { full, half, empty: 5 - full - (half ? 1 : 0) };
	}

	// ---- Mood label map ----
	/** @type {Record<string, string>} */
	const moodLabels = {
		chill: 'Chill / Relax',
		party: 'Fun / Party',
		romantic: 'Romantic',
		family: 'Family',
		work: 'Work / Study',
		foodie: 'Foodie / Trendy'
	};
</script>

<svelte:head>
	<title>Your Curated Results — Chooser</title>
	<meta name="description" content="Hand-picked restaurants matching your mood, budget, and preferences." />
</svelte:head>

<div class="min-h-screen bg-gray-50">
	<div class="max-w-screen-xl mx-auto px-4 sm:px-6 py-8 md:py-12">

		<!-- Header -->
		<div class="mb-8 md:mb-10">
			<a href="/moods" class="fade-in inline-flex items-center gap-1.5 text-purple-600 text-xs font-semibold uppercase tracking-wider hover:text-purple-800 transition-colors mb-4 group">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 transition-transform group-hover:-translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
					<path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
				</svg>
				Back to Moods
			</a>
			<h1 class="fade-in text-3xl md:text-4xl lg:text-5xl font-black tracking-tight text-gray-900 mb-3">
				Your <span class="text-purple-600">Curated</span> Experience.
			</h1>
			<p class="fade-in text-gray-500 text-sm md:text-base max-w-xl leading-relaxed">
				{filteredRestaurants.length} spot{filteredRestaurants.length !== 1 ? 's' : ''} matched your vibe — handpicked for your next adventure.
			</p>

			<!-- Active filters -->
			<div class="flex flex-wrap gap-2 mt-4">
				{#each moodList as m}
					<span class="inline-flex items-center gap-1 px-3 py-1 rounded-full text-xs font-semibold bg-purple-100 text-purple-700">
						{moodLabels[m] || m}
					</span>
				{/each}
				<span class="inline-flex items-center gap-1 px-3 py-1 rounded-full text-xs font-semibold bg-gray-100 text-gray-600">
					₾{budget} budget
				</span>
				{#if solo}
					<span class="inline-flex items-center gap-1 px-3 py-1 rounded-full text-xs font-semibold bg-green-100 text-green-700">Solo Friendly</span>
				{/if}
				{#if outdoor}
					<span class="inline-flex items-center gap-1 px-3 py-1 rounded-full text-xs font-semibold bg-blue-100 text-blue-700">Outdoor</span>
				{/if}
			</div>
		</div>

		<!-- Results Grid -->
		{#if filteredRestaurants.length === 0}
			<div class="fade-in text-center py-20">
				<p class="text-5xl mb-4">🔍</p>
				<h2 class="text-xl font-bold text-gray-900 mb-2">No matches found</h2>
				<p class="text-gray-500 text-sm mb-6">Try adjusting your mood or budget to discover more options.</p>
				<a href="/moods" class="inline-flex px-6 py-3 rounded-xl bg-purple-600 text-white font-semibold text-sm hover:bg-purple-700 transition-colors">
					Adjust Preferences
				</a>
			</div>
		{:else}
			<div class="grid grid-cols-1 md:grid-cols-2 gap-5 md:gap-6 items-start">
				{#each filteredRestaurants as r, i}
					<article
						class="fade-in restaurant-card bg-white rounded-2xl border border-gray-200 overflow-hidden transition-shadow duration-300 hover:shadow-xl"
						style="transition-delay: {i * 80}ms"
					>
						<!-- Image Header -->
						<div class="relative h-48 md:h-56 overflow-hidden">
							<img
								src={r.image}
								alt={r.name}
								class="w-full h-full object-cover transition-transform duration-700 hover:scale-105"
								loading="lazy"
							/>
							<div class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/10 to-transparent"></div>

							<!-- Rating badge -->
							<div class="absolute top-3 left-3 flex items-center gap-1.5 bg-white/95 backdrop-blur-sm px-2.5 py-1 rounded-lg shadow-sm">
								<svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5 text-amber-400" viewBox="0 0 20 20" fill="currentColor">
									<path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
								</svg>
								<span class="text-xs font-bold text-gray-900">{r.rating}</span>
								<span class="text-[10px] text-gray-400">({r.reviews})</span>
							</div>

							<!-- Price badge -->
							<div class="absolute top-3 right-3 bg-purple-600 text-white px-2.5 py-1 rounded-lg text-xs font-bold shadow-sm">
								{r.avgCheck}
							</div>

							<!-- Name overlay -->
							<div class="absolute bottom-0 left-0 right-0 p-4">
								<h2 class="text-white font-bold text-xl md:text-2xl drop-shadow-lg">{r.name}</h2>
								<p class="text-white/80 text-sm font-medium">{r.cuisine}</p>
							</div>
						</div>

						<!-- Card Body -->
						<div class="p-4 md:p-5">
							<!-- Info Row -->
							<div class="flex flex-wrap items-center gap-3 text-xs text-gray-500 mb-3">
								<span class="flex items-center gap-1">
									<svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
										<path stroke-linecap="round" stroke-linejoin="round" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
										<path stroke-linecap="round" stroke-linejoin="round" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
									</svg>
									{r.distance}
								</span>
								<span class="flex items-center gap-1">
									<svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
										<path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
									</svg>
									{r.hours}
								</span>
								<span class="flex items-center gap-1">
									<svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
										<path stroke-linecap="round" stroke-linejoin="round" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
									</svg>
									{r.address}
								</span>
							</div>

							<!-- Tags -->
							<div class="flex flex-wrap gap-1.5 mb-4">
								{#each r.tags as tag}
									<span class="px-2 py-0.5 rounded-md bg-gray-100 text-gray-600 text-[10px] font-semibold uppercase tracking-wider">{tag}</span>
								{/each}
								{#if r.outdoor}
									<span class="px-2 py-0.5 rounded-md bg-green-50 text-green-600 text-[10px] font-semibold uppercase tracking-wider">Outdoor</span>
								{/if}
								{#if r.soloFriendly}
									<span class="px-2 py-0.5 rounded-md bg-blue-50 text-blue-600 text-[10px] font-semibold uppercase tracking-wider">Solo OK</span>
								{/if}
							</div>

							<!-- Expand Menu Button -->
							<button
								on:click={() => toggleExpand(r.id)}
								class="w-full flex items-center justify-between py-2.5 px-4 rounded-xl border border-gray-200 hover:border-purple-300 hover:bg-purple-50/50 transition-all text-sm font-semibold text-gray-700 group"
							>
								<span>{expandedIds.has(r.id) ? 'Hide Menu' : 'View Menu'}</span>
								<svg
									xmlns="http://www.w3.org/2000/svg"
									class="h-4 w-4 text-gray-400 group-hover:text-purple-500 transition-transform duration-300"
									class:rotate-180={expandedIds.has(r.id)}
									fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"
								>
									<path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
								</svg>
							</button>

							<!-- Expandable Menu -->
							{#if expandedIds.has(r.id)}
								<div class="mt-4 space-y-3 menu-reveal">
									<h4 class="text-xs font-bold text-gray-400 uppercase tracking-wider">Popular Dishes</h4>
									{#each r.menu as dish}
										<div class="flex items-center gap-3 p-2 rounded-xl hover:bg-gray-50 transition-colors">
											<img
												src={dish.image}
												alt={dish.name}
												class="w-16 h-12 rounded-lg object-cover flex-shrink-0"
												loading="lazy"
											/>
											<div class="flex-1 min-w-0">
												<p class="text-sm font-semibold text-gray-900 truncate">{dish.name}</p>
											</div>
											<span class="text-sm font-bold text-purple-600 flex-shrink-0">{dish.price}</span>
										</div>
									{/each}
								</div>
							{/if}
						</div>
					</article>
				{/each}
			</div>
		{/if}

		<!-- Bottom CTA -->
		<div class="fade-in text-center mt-12 mb-8">
			<p class="text-gray-400 text-sm mb-4">Not what you're looking for?</p>
			<a href="/moods" class="inline-flex items-center gap-2 px-6 py-3 rounded-xl bg-purple-600 text-white font-semibold text-sm hover:bg-purple-700 transition-all hover:-translate-y-0.5 shadow-lg shadow-purple-200">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
					<path stroke-linecap="round" stroke-linejoin="round" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
				</svg>
				Refine Your Vibes
			</a>
		</div>
	</div>
</div>

<style>
	/* Scroll reveal */
	/* Scroll reveal - auto-play animation */
	.fade-in {
		animation: fadeInUp 0.5s cubic-bezier(0.16, 1, 0.3, 1) both;
	}
	@keyframes fadeInUp {
		from { opacity: 0; transform: translateY(20px); }
		to { opacity: 1; transform: translateY(0); }
	}

	/* Restaurant card hover lift */
	.restaurant-card {
		transition: box-shadow 0.3s ease, transform 0.3s ease;
	}
	.restaurant-card:hover {
		transform: translateY(-2px);
	}

	/* Menu reveal animation */
	.menu-reveal {
		animation: slideDown 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;
	}
	@keyframes slideDown {
		from { opacity: 0; transform: translateY(-8px); }
		to { opacity: 1; transform: translateY(0); }
	}

	/* Chevron rotation */
	.rotate-180 {
		transform: rotate(180deg);
	}

	@media (prefers-reduced-motion: reduce) {
		.fade-in { animation: none; opacity: 1; transform: none; }
		.menu-reveal { animation: none; }
	}
</style>
