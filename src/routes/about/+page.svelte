<script>
	const today = new Date();

	const brickSimple = [new Date(2022, 4), today];
	const ncar = [new Date(2022, 0), new Date(2022, 7)];
	const frtc = [new Date(2019, 4), today];
	const fiske = [new Date(2019, 1), new Date(2022, 4)];
	const boulderMD = [new Date(2022, 7), today];
	const boulderLA = [new Date(2020, 0), new Date(2020, 11)];

	function getMonthsYears(tenure) {
		const duration = new Date(tenure[1] - tenure[0]);
		const years = duration.getUTCFullYear() - 1970;
		const months = duration.getUTCMonth();
		const yearString = years === 1 ? 'year' : 'years';
		const monthString = months === 1 ? 'month' : 'months';

		if (years === 0) return `${months} ${monthString}`;
		if (months === 0) return `${years} ${yearString}`;
		return `${years} ${yearString}, ${months} ${monthString}`;
	}
</script>

<svelte:head>
	<title>Collin Sinclair - About</title>
	<meta
		name="description"
		content="Collin Sinclair is a software engineer and theatre music director/conductor in Denver, CO."
	/>
</svelte:head>

<main class="container">
	<h1 class="text-zinc-200 text-3xl py-3">About</h1>
	<h2 class="text-zinc-200 text-2xl py-2">Experience</h2>
	<ul>
		<li class="py-2">
			<h1 class="text-zinc-200 text-xl">Software Engineer</h1>
			<p class="text-zinc-200 text-lg underline hover:no-underline hover:text-red-600">
				<a href="https://bricksimple.com">BrickSimple, LLC</a>
			</p>
			<p class="text-zinc-200 text-md">May 2022 - Present ({getMonthsYears(brickSimple)})</p>
			<p class="text-zinc-200 text-sm py-2">
				As a software engineer at BrickSimple, I've gained extensive experience in both front-end
				and back-end development while working on various projects for clients. On the front end,
				I've worked with React and Vue to build engaging and intuitive user interfaces. On the back
				end, I've used Django/REST Framework and ASP.NET to create robust and scalable web
				applications.
			</p>
			<p class="text-zinc-200 text-sm pb-2">
				Throughout my tenure, I've been an active participant in agile methodology, collaborating
				with team members to meet project goals and milestones. I've also helped maintain CI/CD
				development, ensuring that code is consistently and reliably deployed to production.
			</p>
			<p class="text-zinc-200 text-sm">
				Overall, my time at BrickSimple has allowed me to develop a well-rounded skill set and a
				deep understanding of the software development life cycle. I look forward to leveraging
				these skills in future opportunities.
			</p>
		</li>
		<hr />
		<li class="py-2">
			<h1 class="text-zinc-200 text-xl">Music Director/Conductor</h1>
			<p class="text-zinc-200 hover:text-amber-300 text-lg underline hover:no-underline">
				<a href="https://colorado.edu">University of Colorado</a>
			</p>
			<p class="text-zinc-200 text-md">Aug 2022 - Present ({getMonthsYears(boulderMD)})</p>
			<ul class="list-disc ml-5 pt-3">
				<li class="text-zinc-200 text-sm">Chicago (Spring 2023)</li>
				<li class="text-zinc-200 text-sm">Drowsy Chaperone (Fall 2022)</li>
				<li class="text-zinc-200 text-sm">Urinetown (Spring 2022)</li>
			</ul>
		</li>
		<hr />
		<li class="py-2">
			<h1 class="text-zinc-200 text-xl">Music Director/Conductor</h1>
			<p class="text-zinc-200 text-lg hover:text-pink-500 underline hover:no-underline">
				<a href="https://frontrangetheatre.org">Front Range Theatre Company</a>
			</p>
			<p class="text-zinc-200 text-md">May 2019 - Present ({getMonthsYears(frtc)})</p>
			<p class="text-zinc-200 text-sm">
				FRTC is a nonprofit educational theatre company that seeks to enrich life through a quality
				performing arts experience. Every summer I work as a music director and lead our students
				through the musical aspects of shows that they put up in just two weeks!
			</p>
			<ul class="list-disc ml-5 pt-3">
				<li class="text-zinc-200 text-sm">Footloose (Summer 2023)</li>
				<li class="text-zinc-200 text-sm">Newsies (Summer 2023)</li>
				<li class="text-zinc-200 text-sm">Mamma Mia (Summer 2022)</li>
				<li class="text-zinc-200 text-sm">Frozen (Summer 2022)</li>
				<li class="text-zinc-200 text-sm">Fame (Summer 2021)</li>
				<li class="text-zinc-200 text-sm">Annie (Summer 2021)</li>
				<li class="text-zinc-200 text-sm">Heathers (Summer 2019)</li>
				<li class="text-zinc-200 text-sm">Aladdin (Summer 2019)</li>
				<li class="text-zinc-200 text-sm">Shrek (Summer 2019)</li>
			</ul>
		</li>
		<hr />
		<li class="py-2">
			<h1 class="text-zinc-200 text-xl">Interactive Web Developer</h1>
			<p class="text-zinc-200 text-lg hover:text-blue-500 underline hover:no-underline">
				<a href="https://ncar.ucar.edu/">NCAR - National Center for Atmospheric Research</a>
			</p>
			<p class="text-zinc-200 text-md">Jan 2022 - Aug 2022 ({getMonthsYears(ncar)})</p>
			<p class="text-zinc-200 text-sm">
				As an interactive web developer with Visualization Services and Research (ViSR) at NCAR, I
				investigated modern web technologies and develop interactive websites that accompany white
				papers, make science more accessible, and expand the horizons of scientific communication
				and research endeavors.
			</p>
			<p class="text-zinc-200 text-sm pt-2">
				Most recently, I focused on creating geographic information interactives, enabling
				researchers to connect with their observed or simulated data in a meaningful way which can
				be shared with anyone who has access to a web browser.
			</p>
		</li>
		<hr />
		<li class="py-2">
			<h1 class="text-zinc-200 text-xl">Presenter, Educator, Podcast Host</h1>
			<p class="text-zinc-200 text-lg hover:text-gray-400 underline hover:no-underline">
				<a href="https://www.colorado.edu/fiske/">Fiske Planetarium</a>
			</p>
			<p class="text-zinc-200 text-md">Feb 2019 - May 2022 ({getMonthsYears(fiske)})</p>
			<p class="text-zinc-200 text-sm">
				As a presenter I delivered live presentations (5-80 minutes, usually one hour) to audiences
				as large as 210 (general public as well as K-12) to communicate scientific points and
				accompany full-dome films or other learning activities. As a part of the process I
				collaborated with fellow planetarians to create and develop scripts which are augmented by
				interactive visualizations and other media on the dome or in the classroom to achieve
				innovating immersive, educational experiences to engage, inspire, and build inclusive
				communities.
			</p>
			<p class="text-zinc-200 text-sm pt-2">
				As a way to maintain engagement and continue to educate when COVID-19 closed Fiske's doors,
				I co-created and co-hosted the official podcast of the Fiske Planetarium: <a
					class="hover:text-gray-300 underline hover:no-underline"
					href="https://www.colorado.edu/fiske/view-earth-fiske-planetarium-podcast"
					>A View From Earth</a
				>. On the show, my co-host and I interviewed working researchers and students from the
				Colorado community to learn about their work and put a face (and voice) to the mind-blowing
				research being done in our backyard!
			</p>
		</li>
		<hr />
		<li class="py-2">
			<h1 class="text-zinc-200 text-xl">Learning Assistant, Mentor</h1>
			<p class="text-zinc-200 text-lg hover:text-amber-300 underline hover:no-underline">
				<a href="https://colorado.edu">University of Colorado</a>
			</p>
			<p class="text-zinc-200 text-md">Jan 2020 - Dec 2020 ({getMonthsYears(boulderLA)})</p>
			<p class="text-zinc-200 text-sm">
				The Learning Assistant program at CU Boulder employs undergraduate students to assist course
				instructional teams in creating optimal learning environments for students. As an LA, I
				facilitated discussions among groups of students in a variety of classroom settings that
				encourage active engagement.
			</p>
			<p class="text-zinc-200 text-sm pt-2">
				Specifically, I worked with the Department of Computer Science in "Starting Computing"
				leading recitations, running review sessions for exams, and holding office hours to consult
				students on their weekly assignments and final projects.
			</p>
			<p class="text-zinc-200 text-sm pt-2">
				Additionally, I worked with the Department of Astrophysical and Planetary Sciences in their
				"Introductory Astronomy" course directing weekly labs and overseeing and guiding nighttime
				observing sessions at the Sommers-Bausch Observatory.
			</p>
			<p class="text-zinc-200 text-sm pt-2">
				Finally, as an LA Mentor, I met with a group of mentees (first-time LAs) on a weekly basis
				for a semester to support their journey as young educators in their pedagogy course as well
				as their LA-student interactions.
			</p>
		</li>
	</ul>
</main>
