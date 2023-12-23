<!-- pages/index.vue -->
<template>
	<div class="mx-8 my-8 mt-8 flex md:mt-16">
		<div class="md:ml-16">
			<h1 class="mb-8 text-center text-3xl font-bold md:text-4xl">
				Generador de <span class="bg-gradient-to-r from-purple-400 to-pink-500 bg-clip-text text-transparent">Nombres Aleatorios</span>
			</h1>
			<div class="md:ml-0">
				<h1 class="mb-4 text-2xl font-semibold">Lenguaje</h1>
				<div class="mb-4 flex space-x-4">
					<button
						@click="selectLanguage('spanish')"
						:class="{
							'border-sky-600': selectedLanguage === 'spanish',
							'border-2 border-black/20 bg-white text-black': selectedLanguage !== 'spanish'
						}"
						class="flex rounded-full border-2 border-black/20 px-4 py-2 focus:outline-none"
					>
						Español
						<img
							width="20"
							height="20"
							class="ml-2 mt-[2px]"
							src="https://img.icons8.com/external-others-iconmarket/64/external-spain-flags-others-iconmarket.png"
							alt="external-spain-flags-others-iconmarket"
						/>
					</button>
					<button
						@click="selectLanguage('english')"
						:class="{
							'border-sky-600': selectedLanguage === 'english',
							'border-2 border-black/20 bg-white text-black': selectedLanguage !== 'english'
						}"
						class="flex rounded-full border-2 border-black/20 px-4 py-2 focus:outline-none"
					>
						Inglés
						<img
							width="20"
							height="20"
							class="ml-2 mt-[2px] rounded-xl"
							src="https://img.icons8.com/color/48/great-britain.png"
							alt="great-britain"
						/>
					</button>
				</div>
				<h1 class="mb-4 text-2xl font-semibold">Género</h1>
				<div class="mb-4 flex space-x-4">
					<button
						@click="selectGender('male')"
						:class="{
							'border-sky-600': selectedGender === 'male',
							'border-2 border-black/20 bg-white text-black': selectedGender !== 'male'
						}"
						class="flex rounded-full border-2 border-black/20 px-4 py-2 focus:outline-none"
					>
						Chico
						<img
							width="20"
							height="20"
							class="ml-[3px] mt-[2px]"
							src="https://img.icons8.com/office/16/male-stroke.png"
							alt="male-stroke"
						/>
					</button>
					<button
						@click="selectGender('female')"
						:class="{
							'border-pink-500': selectedGender === 'female',
							'border-2 border-black/20 bg-white text-black': selectedGender !== 'female'
						}"
						class="flex rounded-full border-2 border-black/20 px-4 py-2 focus:outline-none"
					>
						Chica <img width="24" height="24" src="https://img.icons8.com/emoji/48/female-sign-emoji.png" alt="female-sign-emoji" />
					</button>
				</div>
				<h1 class="mb-4 text-2xl font-semibold">Extras</h1>
				<div class="mb-4 flex space-x-4">
					<label class="flex cursor-pointer items-center space-x-2">
						<input
							v-model="includeCarita"
							type="checkbox"
							class="form-checkbox h-5 w-5 rounded text-blue-500 focus:border-blue-300 focus:outline-none focus:ring"
						/>
						<span>Carita</span>
					</label>
					<label class="flex cursor-pointer items-center space-x-2">
						<input
							v-model="includeNumber"
							type="checkbox"
							class="form-checkbox h-5 w-5 rounded text-blue-500 focus:border-blue-300 focus:outline-none focus:ring"
						/>
						<span>Número</span>
					</label>
					<input
						v-model="customNumber"
						type="number"
						placeholder="Número"
						class="w-[100px] rounded border p-2"
						:class="{ invisible: !includeNumber }"
					/>
				</div>
				<div class="mb-4 flex space-x-4">
					<button
						@click="clapped()"
						:class="{
							'border-sky-600': clappeddd,
							'border-2 border-black/20 bg-white text-black': !clappeddd
						}"
						class="flex rounded-full border-2 border-black/20 px-4 py-2 focus:outline-none"
					>
						<span>Clapped by, Boxxed by, 200 by</span>
					</button>
				</div>
				<div class="mb-4 flex space-x-4">
					<button
						@click="optionss()"
						:class="{
							'border-sky-600': optionsss,
							'border-2 border-black/20 bg-white text-black': !optionsss
						}"
						class="flex rounded-full border-2 border-black/20 px-4 py-2 focus:outline-none"
					>
						<span>HD, PRO, TTV, T.TV, FPS</span>
					</button>
				</div>
				<textarea
					v-model="generatedName"
					class="mb-4 h-11 w-[80%] resize-none overflow-hidden rounded-lg border p-2 text-center sm:w-[100%]"
					readonly
				></textarea>
				<button
					@click="generateName"
					:disabled="!selectedLanguage || !selectedGender"
					class="w-40 rounded bg-green-500 px-4 py-2 text-white sm:mx-auto"
					:class="{ 'cursor-not-allowed opacity-50': !selectedLanguage || !selectedGender }"
				>
					Generar Nombre
				</button>
				<button v-if="generatedName" @click="copyToClipboard" class="ml-4 rounded bg-blue-500 px-4 py-2 text-white">
					Copiar
					<svg
						aria-hidden="true"
						focusable="false"
						role="img"
						viewBox="0 0 16 16"
						width="16"
						height="16"
						fill="currentColor"
						class="mb-1 ml-2 inline-block"
					>
						<path
							d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"
						></path>
						<path
							d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"
						></path>
					</svg>
				</button>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const selectedLanguage = ref('');
const selectedGender = ref('');
const includeCarita = ref(false);
const includeNumber = ref(false);
const customNumber = ref('');
const generatedName = ref('');
const selectedCategories = ref([]);

const Toast = useToast();

const spanishMaleNames = [
	'Alejandro',
	'Santiago',
	'Mateo',
	'Adrián',
	'Diego',
	'Javier',
	'Carlos',
	'Daniel',
	'David',
	'Hugo',
	'Pablo',
	'Manuel',
	'Ángel',
	'Fernando',
	'Luis',
	'Martín',
	'Joaquín',
	'Jorge',
	'Antonio',
	'Miguel',
	'Mario',
	'Francisco',
	'Rubén',
	'Alberto',
	'Ricardo',
	'José',
	'Julio',
	'Iván',
	'Jaime',
	'Óscar',
	'Andrés',
	'Víctor',
	'Rafael',
	'Emilio',
	'Pedro',
	'Tomás',
	'Guillermo',
	'Xavier',
	'Nicolás',
	'Gonzalo',
	'Eduardo',
	'Jesús',
	'Félix',
	'Paco',
	'Jordi',
	'Álvaro',
	'Sergio',
	'César',
	'Juan',
	'Roberto',
	'Enrique',
	'Albert',
	'Alex'
];

const spanishFemaleNames = [
	'Lucía',
	'Sofía',
	'Valentina',
	'Martina',
	'María',
	'Paula',
	'Julia',
	'Daniela',
	'Alejandra',
	'Alba',
	'Emma',
	'Carmen',
	'Ana',
	'Luna',
	'Adriana',
	'Alicia',
	'Elena',
	'Clara',
	'Laura',
	'Marta',
	'Raquel',
	'Nerea',
	'Isabel',
	'Victoria',
	'Patricia',
	'Cristina',
	'Lola',
	'Mireia',
	'Gloria',
	'Lourdes',
	'Silvia',
	'Beatriz',
	'Marina',
	'Natalia',
	'Rocío',
	'Pilar',
	'Carla',
	'Teresa',
	'Montserrat',
	'Ainhoa',
	'Irene',
	'Esther',
	'Olga',
	'Mónica',
	'Rosa',
	'Mercedes',
	'Eva',
	'Miriam',
	'Sara',
	'Lorena',
	'Ángela',
	'Noelia',
	'Aurora',
	'Celia',
	'Belen'
];

const englishMaleNames = [
	'James',
	'John',
	'Robert',
	'Michael',
	'William',
	'David',
	'Richard',
	'Joseph',
	'Thomas',
	'Charles',
	'Christopher',
	'Daniel',
	'Matthew',
	'Anthony',
	'Mark',
	'Donald',
	'Steven',
	'Paul',
	'Andrew',
	'George',
	'Brian',
	'Edward',
	'Ronald',
	'Kenneth',
	'Timothy',
	'Jason',
	'Jeffrey',
	'Ryan',
	'Gary',
	'Nicholas',
	'Eric',
	'Stephen',
	'Jacob',
	'Larry',
	'Frank',
	'Jonathan',
	'Scott',
	'Raymond',
	'Gregory',
	'Joshua',
	'Jerry',
	'Dennis',
	'Walter',
	'Patrick',
	'Peter',
	'Harold',
	'Douglas',
	'Henry',
	'Carl',
	'Arthur',
	'Roger',
	'Joe',
	'Juan',
	'Jack'
];

const englishFemaleNames = [
	'Mary',
	'Patricia',
	'Jennifer',
	'Linda',
	'Elizabeth',
	'Barbara',
	'Susan',
	'Jessica',
	'Sarah',
	'Karen',
	'Nancy',
	'Lisa',
	'Margaret',
	'Betty',
	'Dorothy',
	'Sandra',
	'Ashley',
	'Kimberly',
	'Donna',
	'Emily',
	'Michelle',
	'Carol',
	'Amanda',
	'Melissa',
	'Deborah',
	'Stephanie',
	'Rebecca',
	'Laura',
	'Sharon',
	'Cynthia',
	'Kathleen',
	'Amy',
	'Shirley',
	'Angela',
	'Helen',
	'Anna',
	'Brenda',
	'Pamela',
	'Nicole',
	'Emma',
	'Samantha',
	'Katherine',
	'Christine',
	'Debra',
	'Rachel',
	'Catherine',
	'Carolyn',
	'Janet',
	'Ruth',
	'Maria',
	'Heather',
	'Diane'
];

const selectLanguage = (language) => {
	selectedLanguage.value = language;
};

const selectGender = (gender) => {
	selectedGender.value = gender;
};

const clappeddd = ref(false);

function clapped() {
	toggleCategory('clapped');
	if (clappeddd.value == false) {
		clappeddd.value = true;
	} else {
		clappeddd.value = false;
	}
}

const optionsss = ref(false);

function optionss() {
	toggleCategory('options');
	if (optionsss.value == false) {
		optionsss.value = true;
	} else {
		optionsss.value = false;
	}
}

const copyToClipboard = () => {
	navigator.clipboard.writeText(generatedName.value);
	Toast.success('Nombre copiado al portapapeles!', {
		timeout: 2000,
		closeOnClick: true,
		pauseOnFocusLoss: true,
		pauseOnHover: false,
		draggable: true,
		draggablePercent: 0.6,
		showCloseButtonOnHover: false,
		hideProgressBar: false,
		closeButton: 'button',
		icon: true,
		rtl: false
	});
};

const toggleCategory = (category) => {
	if (selectedCategories.value.includes(category)) {
		// Si ya está seleccionado, quitarlo
		selectedCategories.value = selectedCategories.value.filter((c) => c !== category);
	} else {
		// Si no está seleccionado, agregarlo
		selectedCategories.value.push(category);
	}
};

const generateNameForClappedCategory = (name) => {
	const clappedOptions = ['clapped by ', 'boxxed by ', '200 by '];
	const randomOption = clappedOptions[Math.floor(Math.random() * clappedOptions.length)];
	return name + randomOption;
};

const generateNameForOptionsCategory = (name) => {
	const options = ['HD', 'PRO', 'TTV', 'T.TV', 'FPS'];
	const randomOption = options[Math.floor(Math.random() * options.length)];
	return name + randomOption;
};
const generateNameForOptionsAndClappedCategory = (name) => {
	const options = ['HD', 'PRO', 'TTV', 'T.TV', 'FPS'];
	const clappedOptions = ['clapped by ', 'boxxed by ', '200 by '];
	const randomBy = clappedOptions[Math.floor(Math.random() * clappedOptions.length)];
	const randomOption = options[Math.floor(Math.random() * options.length)];
	return name + randomBy + randomOption;
};

const generateCarita = () => {
	const caritas = ['UwU', 'ツ', '-_-', 'OwO'];
	return includeCarita.value ? caritas[Math.floor(Math.random() * caritas.length)] : '';
};

const generateRealName = (language, gender) => {
	let namesArray = [];

	if (language === 'spanish' && gender === 'male') {
		namesArray = spanishMaleNames;
	} else if (language === 'spanish' && gender === 'female') {
		namesArray = spanishFemaleNames;
	} else if (language === 'english' && gender === 'male') {
		namesArray = englishMaleNames;
	} else if (language === 'english' && gender === 'female') {
		namesArray = englishFemaleNames;
	}

	const randomName = namesArray[Math.floor(Math.random() * namesArray.length)];
	return randomName;
};

const generateName = () => {
	let finalName = '';

	if (selectedCategories.value.includes('clapped') && selectedCategories.value.includes('options')) {
		const primero = generateNameForClappedCategory(finalName);
		const segundo = generateRealName(selectedLanguage.value, selectedGender.value);
		const tercero = generateNameForOptionsCategory(finalName);
		finalName = primero + segundo + tercero;
	} else if (selectedCategories.value.includes('clapped')) {
		finalName += generateNameForClappedCategory(finalName);
		finalName += generateRealName(selectedLanguage.value, selectedGender.value);
	} else if (selectedCategories.value.includes('options')) {
		finalName += generateNameForOptionsCategory(finalName);
		const nombreee = generateRealName(selectedLanguage.value, selectedGender.value);
		finalName = nombreee + finalName;
	} else {
		finalName += generateRealName(selectedLanguage.value, selectedGender.value);
	}

	finalName += includeNumber.value ? customNumber.value || Math.floor(Math.random() * 100) : '';
	finalName += generateCarita();

	generatedName.value = finalName;
	Toast.success('Nombre generado con éxito!', {
		timeout: 2000,
		closeOnClick: true,
		pauseOnFocusLoss: true,
		pauseOnHover: false,
		draggable: true,
		draggablePercent: 0.6,
		showCloseButtonOnHover: false,
		hideProgressBar: false,
		closeButton: 'button',
		icon: true,
		rtl: false
	});
};
</script>
