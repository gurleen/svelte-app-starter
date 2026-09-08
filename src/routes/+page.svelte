<script lang="ts">
	import { Button } from "$lib/components/ui/button/index.js";
	import { Badge } from "$lib/components/ui/badge/index.js";
	import { Input } from "$lib/components/ui/input/index.js";
	import { Label } from "$lib/components/ui/label/index.js";
	import * as Card from "$lib/components/ui/card/index.js";
	import { Checkbox } from "$lib/components/ui/checkbox/index.js";
	import { Switch } from "$lib/components/ui/switch/index.js";
	import * as Tabs from "$lib/components/ui/tabs/index.js";
	import * as Select from "$lib/components/ui/select/index.js";
	import * as Dialog from "$lib/components/ui/dialog/index.js";
	import * as DropdownMenu from "$lib/components/ui/dropdown-menu/index.js";
	import * as Tooltip from "$lib/components/ui/tooltip/index.js";
	import * as Table from "$lib/components/ui/table/index.js";
	import { Separator } from "$lib/components/ui/separator/index.js";

	let dark = $state(false);

	$effect(() => {
		document.documentElement.classList.toggle("dark", dark);
	});

	const fruit = ["Apple", "Banana", "Cherry"];
	let selectedFruit = $state("Apple");

	const invoices = [
		{ id: "INV001", status: "Paid", amount: "$250.00" },
		{ id: "INV002", status: "Pending", amount: "$150.00" },
		{ id: "INV003", status: "Overdue", amount: "$350.00" },
	];
</script>

<Tooltip.Provider>
	<div class="mx-auto max-w-4xl space-y-12 p-8">
		<div class="flex items-center justify-between">
			<h1 class="text-lg font-semibold">Blueprint component showcase</h1>
			<Button variant="outline" size="sm" onclick={() => (dark = !dark)}>
				{dark ? "Switch to light" : "Switch to dark"}
			</Button>
		</div>

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Buttons</h2>
			<div class="flex flex-wrap gap-2">
				<Button variant="default">Default</Button>
				<Button variant="outline">Outline</Button>
				<Button variant="secondary">Secondary</Button>
				<Button variant="ghost">Ghost</Button>
				<Button variant="destructive">Destructive</Button>
				<Button variant="success">Success</Button>
				<Button variant="warning">Warning</Button>
				<Button variant="link">Link</Button>
			</div>
			<div class="flex flex-wrap items-center gap-2">
				<Button size="xs">Extra small</Button>
				<Button size="sm">Small</Button>
				<Button size="default">Default</Button>
				<Button size="lg">Large</Button>
				<Button disabled>Disabled</Button>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Badges</h2>
			<div class="flex flex-wrap gap-2">
				<Badge variant="default">Default</Badge>
				<Badge variant="secondary">Secondary</Badge>
				<Badge variant="outline">Outline</Badge>
				<Badge variant="destructive">Destructive</Badge>
				<Badge variant="success">Success</Badge>
				<Badge variant="warning">Warning</Badge>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Inputs</h2>
			<div class="grid max-w-sm gap-3">
				<div class="grid gap-1.5">
					<Label for="email">Email</Label>
					<Input id="email" type="email" placeholder="you@example.com" />
				</div>
				<div class="grid gap-1.5">
					<Label for="disabled-input">Disabled</Label>
					<Input id="disabled-input" placeholder="Disabled" disabled />
				</div>
				<div class="grid gap-1.5">
					<Label for="invalid-input">Invalid</Label>
					<Input id="invalid-input" aria-invalid="true" value="bad value" />
				</div>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Checkbox &amp; Switch</h2>
			<div class="flex items-center gap-6">
				<div class="flex items-center gap-2">
					<Checkbox id="terms" />
					<Label for="terms">Accept terms</Label>
				</div>
				<div class="flex items-center gap-2">
					<Switch id="notifications" />
					<Label for="notifications">Notifications</Label>
				</div>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Select</h2>
			<Select.Root type="single" bind:value={selectedFruit}>
				<Select.Trigger class="w-48">
					{selectedFruit}
				</Select.Trigger>
				<Select.Content>
					{#each fruit as item (item)}
						<Select.Item value={item}>{item}</Select.Item>
					{/each}
				</Select.Content>
			</Select.Root>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Tabs</h2>
			<Tabs.Root value="account" class="max-w-sm">
				<Tabs.List>
					<Tabs.Trigger value="account">Account</Tabs.Trigger>
					<Tabs.Trigger value="password">Password</Tabs.Trigger>
				</Tabs.List>
				<Tabs.Content value="account">Account settings go here.</Tabs.Content>
				<Tabs.Content value="password">Password settings go here.</Tabs.Content>
			</Tabs.Root>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Card</h2>
			<Card.Root class="max-w-sm">
				<Card.Header>
					<Card.Title>Create project</Card.Title>
					<Card.Description>Deploy a new project in one click.</Card.Description>
				</Card.Header>
				<Card.Content>
					<div class="grid gap-1.5">
						<Label for="project-name">Name</Label>
						<Input id="project-name" placeholder="My project" />
					</div>
				</Card.Content>
				<Card.Footer class="justify-end gap-2">
					<Button variant="outline">Cancel</Button>
					<Button>Deploy</Button>
				</Card.Footer>
			</Card.Root>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Table</h2>
			<Table.Root>
				<Table.Header>
					<Table.Row>
						<Table.Head>Invoice</Table.Head>
						<Table.Head>Status</Table.Head>
						<Table.Head class="text-right">Amount</Table.Head>
					</Table.Row>
				</Table.Header>
				<Table.Body>
					{#each invoices as invoice (invoice.id)}
						<Table.Row>
							<Table.Cell>{invoice.id}</Table.Cell>
							<Table.Cell>{invoice.status}</Table.Cell>
							<Table.Cell class="text-right">{invoice.amount}</Table.Cell>
						</Table.Row>
					{/each}
				</Table.Body>
			</Table.Root>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Dialog &amp; Dropdown Menu</h2>
			<div class="flex gap-2">
				<Dialog.Root>
					<Dialog.Trigger>
						{#snippet child({ props })}
							<Button variant="outline" {...props}>Open dialog</Button>
						{/snippet}
					</Dialog.Trigger>
					<Dialog.Content>
						<Dialog.Header>
							<Dialog.Title>Are you sure?</Dialog.Title>
							<Dialog.Description>This action cannot be undone.</Dialog.Description>
						</Dialog.Header>
						<Dialog.Footer>
							<Dialog.Close>
								{#snippet child({ props })}
									<Button variant="outline" {...props}>Cancel</Button>
								{/snippet}
							</Dialog.Close>
							<Button variant="destructive">Delete</Button>
						</Dialog.Footer>
					</Dialog.Content>
				</Dialog.Root>

				<DropdownMenu.Root>
					<DropdownMenu.Trigger>
						{#snippet child({ props })}
							<Button variant="outline" {...props}>Open menu</Button>
						{/snippet}
					</DropdownMenu.Trigger>
					<DropdownMenu.Content>
						<DropdownMenu.Item>Profile</DropdownMenu.Item>
						<DropdownMenu.Item>Settings</DropdownMenu.Item>
						<DropdownMenu.Separator />
						<DropdownMenu.Item>Log out</DropdownMenu.Item>
					</DropdownMenu.Content>
				</DropdownMenu.Root>

				<Tooltip.Root>
					<Tooltip.Trigger>
						{#snippet child({ props })}
							<Button variant="ghost" {...props}>Hover me</Button>
						{/snippet}
					</Tooltip.Trigger>
					<Tooltip.Content>Blueprint-styled tooltip</Tooltip.Content>
				</Tooltip.Root>
			</div>
		</section>
	</div>
</Tooltip.Provider>
