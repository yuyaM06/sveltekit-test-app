<script lang="ts">
	const foxEndPoint = 'https://randomfox.ca/api/v1/getfoxes/';
	const nameEndPoint = 'https://randomuser.me/api/';
	const numOfFox = 18;

	/**
	 * @type {any[]}
	 */
	let foxes = [];

	let fetchImage = (async () => {
		const response = await fetch(foxEndPoint + '?count=' + numOfFox);
		const data = await response.json();
		return data.images;
	})();

	let fetchName = (async () => {
		const response = await fetch(nameEndPoint + '?results=' + numOfFox);
		const data = await response.json();
		return data.results;
	})();

	function randomPos() {
		const posList = ['Chef', 'SEO', 'CTO', 'Designer', 'Architect', 'Engineer'];
		const pos = [];
		for (let i = 0; i < numOfFox; i++)
			pos.push(posList[Math.floor(Math.random() * posList.length)]);
		return pos;
	}

	const getFoxes = (async () => {
		let imgs = await fetchImage;
		let names = await fetchName;
		let poses = randomPos();

		for (let i = 0; i < numOfFox; i++) {
			foxes.push({
				imgSrc: imgs[i],
				name: names[i].name.first + ' ' + names[i].name.last,
				pos: poses[i]
			});
		}
		return await foxes;
	})();
</script>

{#await getFoxes}
	<p>...waiting</p>
{:then foxes}
	<div class="p-8 bg-white shadow dark:bg-gray-800">
		<p class="text-3xl font-bold text-center text-gray-800 dark:text-white">The big team</p>
		<p class="mb-12 text-xl font-normal text-center text-gray-500 dark:text-gray-300">
			Meat the best team in world
		</p>
		<div class="grid grid-cols-2 gap-4 sm:grid-cols-3 lg:grid-cols-6">
			{#each foxes as fox}
				<div class="p-4">
					<div class="flex-col  flex justify-center items-center">
						<div class="flex-shrink-0">
							<a href="#" class="relative block">
								<img
									alt="profil"
									src={fox.imgSrc}
									class="mx-auto object-cover rounded-full h-20 w-20 "
								/>
							</a>
						</div>
						<div class="mt-2 text-center flex flex-col">
							<span class="text-lg font-medium text-gray-600 dark:text-white"> {fox.name} </span>
							<span class="text-xs text-gray-400"> {fox.pos} </span>
						</div>
					</div>
				</div>
			{/each}
			<!-- <div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img alt="profil" src={imgSrc} class="mx-auto object-cover rounded-full h-20 w-20 " />
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> {name} </span>
					<span class="text-xs text-gray-400"> {pos} </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/5.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Igor Novak </span>
					<span class="text-xs text-gray-400"> Designer </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/6.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Jig sa Hiut </span>
					<span class="text-xs text-gray-400"> Boucher </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/7.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Norman Tuck </span>
					<span class="text-xs text-gray-400"> Architect </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/8.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Masrt kik </span>
					<span class="text-xs text-gray-400"> Chef </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/9.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Louis Bol </span>
					<span class="text-xs text-gray-400"> Sdf </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/10.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Izno god </span>
					<span class="text-xs text-gray-400"> American </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/1.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Serena Quille </span>
					<span class="text-xs text-gray-400"> Designer </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/6.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Edouard Sert </span>
					<span class="text-xs text-gray-400"> Developer </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/8.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Parki Son </span>
					<span class="text-xs text-gray-400"> Designer </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/9.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Marine Lo </span>
					<span class="text-xs text-gray-400"> SEO </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/4.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Mickal Poul </span>
					<span class="text-xs text-gray-400"> Freelance </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/5.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Isac Tou </span>
					<span class="text-xs text-gray-400"> Freelance </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/6.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Jean Eu </span>
					<span class="text-xs text-gray-400"> Designer </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/9.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Yves P </span>
					<span class="text-xs text-gray-400"> Humor </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/1.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Marco Tol </span>
					<span class="text-xs text-gray-400"> Designer </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/6.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Huge Ar </span>
					<span class="text-xs text-gray-400"> CEA </span>
				</div>
			</div>
		</div>
		<div class="p-4">
			<div class="flex-col  flex justify-center items-center">
				<div class="flex-shrink-0">
					<a href="#" class="relative block">
						<img
							alt="profil"
							src="/images/person/8.jpg"
							class="mx-auto object-cover rounded-full h-20 w-20 "
						/>
					</a>
				</div>
				<div class="mt-2 text-center flex flex-col">
					<span class="text-lg font-medium text-gray-600 dark:text-white"> Big Bro </span>
					<span class="text-xs text-gray-400"> CTO </span>
				</div>
			</div>
		</div> -->
		</div>
	</div>
{/await}
