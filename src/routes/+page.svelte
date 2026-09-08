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
	import * as Alert from "$lib/components/ui/alert/index.js";
	import * as AlertDialog from "$lib/components/ui/alert-dialog/index.js";
	import * as Breadcrumb from "$lib/components/ui/breadcrumb/index.js";
	import * as Collapsible from "$lib/components/ui/collapsible/index.js";
	import { RadioGroup, RadioGroupItem } from "$lib/components/ui/radio-group/index.js";
	import { Progress } from "$lib/components/ui/progress/index.js";
	import * as ContextMenu from "$lib/components/ui/context-menu/index.js";
	import * as Popover from "$lib/components/ui/popover/index.js";
	import { Textarea } from "$lib/components/ui/textarea/index.js";
	import { Icon } from "$lib/components/ui/icon/index.js";
	import { NonIdealState } from "$lib/components/ui/non-ideal-state/index.js";
	import { ControlGroup } from "$lib/components/ui/control-group/index.js";
	import { toast } from "$lib/components/ui/sonner/index.js";
	import { config } from "$lib/config.svelte";
	import { Search, Settings, Trash2, Inbox } from "@lucide/svelte";

	const fruit = ["Apple", "Banana", "Cherry"];
	let selectedFruit = $state("Apple");

	const invoices = [
		{ id: "INV001", status: "Paid", amount: "$250.00" },
		{ id: "INV002", status: "Pending", amount: "$150.00" },
		{ id: "INV003", status: "Overdue", amount: "$350.00" },
	];

	let radioValue = $state("a");
</script>

<Tooltip.Provider>
	<div class="mx-auto max-w-4xl space-y-12 p-8">
		<div class="flex items-center justify-between">
			<h1 class="text-lg font-semibold">Blueprint component showcase</h1>
			<Button variant="outline" size="sm" onclick={() => config.toggleColorScheme()}>
				{config.colorScheme === "dark" ? "Switch to light" : "Switch to dark"}
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
		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Alert</h2>
			<div class="grid max-w-sm gap-3">
				<Alert.Root>
					<Alert.Title>Heads up</Alert.Title>
					<Alert.Description>This is a default callout.</Alert.Description>
				</Alert.Root>
				<Alert.Root variant="destructive">
					<Alert.Title>Something went wrong</Alert.Title>
					<Alert.Description>This is a tinted destructive callout.</Alert.Description>
				</Alert.Root>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Breadcrumb</h2>
			<Breadcrumb.Root>
				<Breadcrumb.List>
					<Breadcrumb.Item><Breadcrumb.Link href="#">Home</Breadcrumb.Link></Breadcrumb.Item>
					<Breadcrumb.Separator />
					<Breadcrumb.Item><Breadcrumb.Link href="#">Components</Breadcrumb.Link></Breadcrumb.Item>
					<Breadcrumb.Separator />
					<Breadcrumb.Item><Breadcrumb.Page>Current</Breadcrumb.Page></Breadcrumb.Item>
				</Breadcrumb.List>
			</Breadcrumb.Root>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Collapsible</h2>
			<Collapsible.Root class="max-w-sm">
				<Collapsible.Trigger>
					{#snippet child({ props })}
						<Button variant="outline" size="sm" {...props}>Toggle details</Button>
					{/snippet}
				</Collapsible.Trigger>
				<Collapsible.Content class="pt-2 text-xs text-muted-foreground">
					Additional detail revealed by the collapsible.
				</Collapsible.Content>
			</Collapsible.Root>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Radio Group &amp; Progress</h2>
			<div class="flex flex-wrap items-start gap-12">
				<RadioGroup bind:value={radioValue}>
					<div class="flex items-center gap-2">
						<RadioGroupItem value="a" id="radio-a" />
						<Label for="radio-a">Option A</Label>
					</div>
					<div class="flex items-center gap-2">
						<RadioGroupItem value="b" id="radio-b" />
						<Label for="radio-b">Option B</Label>
					</div>
				</RadioGroup>
				<Progress value={45} class="w-48" />
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">
				Context Menu, Popover &amp; Alert Dialog
			</h2>
			<div class="flex flex-wrap items-center gap-2">
				<ContextMenu.Root>
					<ContextMenu.Trigger
						class="flex h-16 w-40 items-center justify-center border border-border text-xs text-muted-foreground"
					>
						Right click me
					</ContextMenu.Trigger>
					<ContextMenu.Content>
						<ContextMenu.Item>Profile</ContextMenu.Item>
						<ContextMenu.Item>Settings</ContextMenu.Item>
						<ContextMenu.Separator />
						<ContextMenu.Item>Log out</ContextMenu.Item>
					</ContextMenu.Content>
				</ContextMenu.Root>

				<Popover.Root>
					<Popover.Trigger>
						{#snippet child({ props })}
							<Button variant="outline" {...props}>Open popover</Button>
						{/snippet}
					</Popover.Trigger>
					<Popover.Content>
						<Popover.Title>Popover title</Popover.Title>
						<Popover.Description>Popover body text.</Popover.Description>
					</Popover.Content>
				</Popover.Root>

				<AlertDialog.Root>
					<AlertDialog.Trigger>
						{#snippet child({ props })}
							<Button variant="destructive" {...props}>Delete account</Button>
						{/snippet}
					</AlertDialog.Trigger>
					<AlertDialog.Content>
						<AlertDialog.Header>
							<AlertDialog.Title>Are you sure?</AlertDialog.Title>
							<AlertDialog.Description>This action cannot be undone.</AlertDialog.Description>
						</AlertDialog.Header>
						<AlertDialog.Footer>
							<AlertDialog.Cancel>
								{#snippet child({ props })}
									<Button variant="outline" {...props}>Cancel</Button>
								{/snippet}
							</AlertDialog.Cancel>
							<AlertDialog.Action>
								{#snippet child({ props })}
									<Button variant="destructive" {...props}>Confirm</Button>
								{/snippet}
							</AlertDialog.Action>
						</AlertDialog.Footer>
					</AlertDialog.Content>
				</AlertDialog.Root>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Textarea</h2>
			<div class="grid max-w-sm gap-1.5">
				<Label for="message">Message</Label>
				<Textarea id="message" placeholder="Type your message here" />
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Icon &amp; Icon Button</h2>
			<div class="flex flex-wrap items-center gap-4">
				<Icon icon={Search} />
				<Icon icon={Settings} intent="primary" />
				<Icon icon={Trash2} intent="danger" size="large" />
				<Button variant="outline" size="icon" aria-label="Search">
					<Icon icon={Search} />
				</Button>
				<Button variant="ghost" size="icon-sm" aria-label="Settings">
					<Icon icon={Settings} />
				</Button>
				<Button variant="destructive" size="icon-lg" aria-label="Delete">
					<Icon icon={Trash2} />
				</Button>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Non-Ideal State</h2>
			<div class="max-w-sm border border-border">
				<NonIdealState
					icon={Inbox}
					title="No results"
					description="Try adjusting your filters or search terms."
				>
					{#snippet action()}
						<Button variant="outline" size="sm">Clear filters</Button>
					{/snippet}
				</NonIdealState>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Control Group</h2>
			<div class="flex flex-wrap items-start gap-6">
				<ControlGroup>
					<Button variant="outline">Left</Button>
					<Button variant="outline">Middle</Button>
					<Button variant="outline">Right</Button>
				</ControlGroup>

				<ControlGroup>
					<Button variant="outline" size="icon" aria-label="Search">
						<Icon icon={Search} />
					</Button>
					<Input placeholder="Search…" class="w-48" />
				</ControlGroup>

				<ControlGroup vertical>
					<Button variant="outline">Top</Button>
					<Button variant="outline">Bottom</Button>
				</ControlGroup>
			</div>
		</section>

		<Separator />

		<section class="space-y-3">
			<h2 class="text-sm font-semibold text-muted-foreground">Toast</h2>
			<div class="flex flex-wrap gap-2">
				<Button variant="outline" onclick={() => toast("Event has been created")}>Default</Button
				>
				<Button
					variant="outline"
					onclick={() => toast.success("Changes saved", { description: "Your profile is up to date." })}
					>Success</Button
				>
				<Button
					variant="outline"
					onclick={() => toast.warning("Storage almost full", { description: "You are at 90% of your quota." })}
					>Warning</Button
				>
				<Button
					variant="outline"
					onclick={() => toast.error("Upload failed", { description: "Check your connection and try again." })}
					>Error</Button
				>
				<Button
					variant="outline"
					onclick={() =>
						toast("New message", {
							description: "You have an unread message from support.",
							action: { label: "View", onClick: () => toast("Opened message") },
						})}>With action</Button
				>
			</div>
		</section>
	</div>
</Tooltip.Provider>
