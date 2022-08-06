<script>
	export let name;
	import Header from './components/Header.svelte'
	import Footer from './components/Footer.svelte'
	import Nav from './shared/Nav.svelte'
	import AddPoll from './components/AddPoll.svelte';
	import PollList from './components/PollList.svelte'

	//navs
	let items = ['Current Polls', 'Add New Polls']
	let active_item = 'Current Polls' 

	const handleTabChange = (e) => {
		active_item = e.detail
	}

	let polls = [
		{
			id: 1,
			question: 'React or svelte',
			ansA: 'React',
			ansB: 'Svelte',
			votesA: 10,
			votesB: 10
		},
	]

	const addPoll = (e) => {
		const newPoll = e.detail
		polls = [...polls, newPoll]
		active_item = 'Current Polls'
	}

	const handleVoting = (e) => {
		const {option , id} = e.detail
		//console.log(Option);
		let copies = [...polls]
		let updatePoll = copies.find((poll) => poll.id === id)

		if(option === 'a') {
			updatePoll.votesA+=1;
		}

		if(option === 'b') {
			updatePoll.votesB+=1;
		}

		polls = copies
	}
</script>

<main>
	<Header />
	<Nav {items} {active_item} on:tabChange={handleTabChange} />
	<h1>Hello {name}!</h1>
	{#if active_item === 'Current Polls'}
		<PollList {polls} on:vote={handleVoting}/>
	{:else}
		<AddPoll on:add={addPoll}/>
	{/if}
	<Footer />
</main>

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>