/*
 * IRHW3.java
 *
 * Created on Nov 6, 2009, 3:21:06 PM
 */
package org.edwardtoday.fulltext;

import java.awt.event.KeyEvent;
import java.io.IOException;
import java.util.ArrayList;
import java.util.logging.Level;
import java.util.logging.Logger;

/**
 * 
 * @author edwardtoday
 */
public class IRHW3 extends javax.swing.JFrame {

	/**
     *
     */
	private static final long serialVersionUID = 2159790484286577399L;

	/**
	 * @param args
	 *            the command line arguments
	 */
	public static void main(final String args[]) {
		java.awt.EventQueue.invokeLater(new Runnable() {

			public void run() {
				new IRHW3().setVisible(true);
			}
		});
	}

	public IRHW3() {
		this.initComponents();
	}

	private void initButtonActionPerformed(final java.awt.event.ActionEvent evt) {
		try {
			LoadData.init();
			this.linearTime.setText(Double.toString(LoadData.wordSearchTime));
			this.indexedTime.setText(Double
					.toString(LoadData.indexedSearchTime));
			this.wordRes.setText(Double.toString(LoadData.wordResults));
			this.charRes.setText(Double.toString(LoadData.charResults));
		} catch (final IOException ex) {
			Logger.getLogger(IRHW3.class.getName()).log(Level.SEVERE, null, ex);
		}
	}

	private void initComponents() {

		this.queryBox = new javax.swing.JTextField();
		this.queryBoxLabel = new javax.swing.JLabel();
		this.resultPanel = new javax.swing.JScrollPane();
		this.resultList = new javax.swing.JList();
		this.linearLabel = new javax.swing.JLabel();
		this.indexedLabel = new javax.swing.JLabel();
		this.timeLabel = new javax.swing.JLabel();
		this.resultsLable = new javax.swing.JLabel();
		this.linearTime = new javax.swing.JLabel();
		this.wordRes = new javax.swing.JLabel();
		this.indexedTime = new javax.swing.JLabel();
		this.charRes = new javax.swing.JLabel();
		this.searchButton = new javax.swing.JButton();
		this.initButton = new javax.swing.JButton();
		this.jScrollPane1 = new javax.swing.JScrollPane();
		this.preview = new javax.swing.JTextArea();
		this.URILabel = new javax.swing.JLabel();
		this.URIfield = new javax.swing.JTextField();

		this
				.setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
		this.setTitle("全文检索算法比较");

		this.queryBox.addKeyListener(new java.awt.event.KeyListener() {

			public void keyPressed(final KeyEvent e) {
				// TODO Auto-generated method stub
			}

			public void keyReleased(final KeyEvent e) {
				// TODO Auto-generated method stub
				if (e.getKeyCode() == KeyEvent.VK_ENTER) {
					IRHW3.this.searchButtonActionPerformed(null);
				}
			}

			public void keyTyped(final KeyEvent e) {
				// TODO Auto-generated method stub
			}
		});

		this.queryBox.addActionListener(new java.awt.event.ActionListener() {

			public void actionPerformed(final java.awt.event.ActionEvent evt) {
				IRHW3.this.queryBoxActionPerformed(evt);
			}
		});

		this.queryBoxLabel.setText("Query:");

		this.resultList.setBorder(javax.swing.BorderFactory
				.createTitledBorder("Result docs"));
		this.resultList
				.addListSelectionListener(new javax.swing.event.ListSelectionListener() {

					public void valueChanged(
							final javax.swing.event.ListSelectionEvent evt) {
						IRHW3.this.resultListValueChanged(evt);
					}
				});
		this.resultPanel.setViewportView(this.resultList);

		this.linearLabel.setText("Word Index");

		this.indexedLabel.setText("Char Index");

		this.timeLabel.setText("Time(ns)");

		this.resultsLable.setText("Mem(KB)");

		this.linearTime.setText("word time");

		this.wordRes.setText("");

		this.indexedTime.setText("indexed time");

		this.charRes.setText("");

		this.searchButton.setText("Search");
		this.searchButton
				.addActionListener(new java.awt.event.ActionListener() {

					public void actionPerformed(
							final java.awt.event.ActionEvent evt) {
						IRHW3.this.searchButtonActionPerformed(evt);
					}
				});

		this.initButton.setText("Init");
		this.initButton.addActionListener(new java.awt.event.ActionListener() {

			public void actionPerformed(final java.awt.event.ActionEvent evt) {
				IRHW3.this.initButtonActionPerformed(evt);
			}
		});

		this.preview.setColumns(20);
		this.preview.setRows(5);
		this.preview.setBorder(javax.swing.BorderFactory
				.createTitledBorder("Preview"));
		this.jScrollPane1.setViewportView(this.preview);

		this.URILabel.setText("URI:");

		this.URIfield.setEditable(false);
		this.URIfield.addActionListener(new java.awt.event.ActionListener() {

			public void actionPerformed(final java.awt.event.ActionEvent evt) {
				IRHW3.this.URIfieldActionPerformed(evt);
			}
		});

		final javax.swing.GroupLayout layout = new javax.swing.GroupLayout(this
				.getContentPane());
		this.getContentPane().setLayout(layout);
		layout
				.setHorizontalGroup(layout
						.createParallelGroup(
								javax.swing.GroupLayout.Alignment.LEADING)
						.addGroup(
								layout
										.createSequentialGroup()
										.addGap(23, 23, 23)
										.addGroup(
												layout
														.createParallelGroup(
																javax.swing.GroupLayout.Alignment.LEADING)
														.addGroup(
																layout
																		.createSequentialGroup()
																		.addComponent(
																				this.queryBoxLabel)
																		.addGap(
																				18,
																				18,
																				18)
																		.addComponent(
																				this.queryBox,
																				javax.swing.GroupLayout.PREFERRED_SIZE,
																				199,
																				javax.swing.GroupLayout.PREFERRED_SIZE)
																		.addGap(
																				18,
																				18,
																				18)
																		.addComponent(
																				this.searchButton)
																		.addGap(
																				18,
																				18,
																				18)
																		.addComponent(
																				this.initButton))
														.addGroup(
																layout
																		.createSequentialGroup()
																		.addPreferredGap(
																				javax.swing.LayoutStyle.ComponentPlacement.RELATED)
																		.addComponent(
																				this.resultPanel,
																				javax.swing.GroupLayout.PREFERRED_SIZE,
																				117,
																				javax.swing.GroupLayout.PREFERRED_SIZE)
																		.addGroup(
																				layout
																						.createParallelGroup(
																								javax.swing.GroupLayout.Alignment.LEADING)
																						.addGroup(
																								layout
																										.createSequentialGroup()
																										.addGap(
																												18,
																												18,
																												18)
																										.addGroup(
																												layout
																														.createParallelGroup(
																																javax.swing.GroupLayout.Alignment.LEADING)
																														.addComponent(
																																this.jScrollPane1,
																																javax.swing.GroupLayout.Alignment.TRAILING,
																																javax.swing.GroupLayout.DEFAULT_SIZE,
																																422,
																																Short.MAX_VALUE)
																														.addGroup(
																																layout
																																		.createSequentialGroup()
																																		.addComponent(
																																				this.URILabel)
																																		.addGap(
																																				18,
																																				18,
																																				18)
																																		.addComponent(
																																				this.URIfield,
																																				javax.swing.GroupLayout.DEFAULT_SIZE,
																																				379,
																																				Short.MAX_VALUE))))
																						.addGroup(
																								layout
																										.createSequentialGroup()
																										.addGap(
																												48,
																												48,
																												48)
																										.addGroup(
																												layout
																														.createParallelGroup(
																																javax.swing.GroupLayout.Alignment.LEADING)
																														.addComponent(
																																this.resultsLable)
																														.addComponent(
																																this.timeLabel))
																										.addGroup(
																												layout
																														.createParallelGroup(
																																javax.swing.GroupLayout.Alignment.LEADING,
																																false)
																														.addGroup(
																																layout
																																		.createSequentialGroup()
																																		.addGap(
																																				54,
																																				54,
																																				54)
																																		.addComponent(
																																				this.wordRes,
																																				javax.swing.GroupLayout.DEFAULT_SIZE,
																																				javax.swing.GroupLayout.DEFAULT_SIZE,
																																				Short.MAX_VALUE))
																														.addGroup(
																																layout
																																		.createSequentialGroup()
																																		.addGap(
																																				55,
																																				55,
																																				55)
																																		.addGroup(
																																				layout
																																						.createParallelGroup(
																																								javax.swing.GroupLayout.Alignment.LEADING)
																																						.addComponent(
																																								this.linearLabel)
																																						.addComponent(
																																								this.linearTime,
																																								javax.swing.GroupLayout.PREFERRED_SIZE,
																																								90,
																																								javax.swing.GroupLayout.PREFERRED_SIZE))))
																										.addGap(
																												45,
																												45,
																												45)
																										.addGroup(
																												layout
																														.createParallelGroup(
																																javax.swing.GroupLayout.Alignment.LEADING)
																														.addComponent(
																																this.indexedLabel)
																														.addGroup(
																																layout
																																		.createSequentialGroup()
																																		.addGap(
																																				2,
																																				2,
																																				2)
																																		.addComponent(
																																				this.charRes))
																														.addComponent(
																																this.indexedTime))))))
										.addGap(17, 17, 17)));
		layout
				.setVerticalGroup(layout
						.createParallelGroup(
								javax.swing.GroupLayout.Alignment.LEADING)
						.addGroup(
								layout
										.createSequentialGroup()
										.addGap(46, 46, 46)
										.addGroup(
												layout
														.createParallelGroup(
																javax.swing.GroupLayout.Alignment.BASELINE)
														.addComponent(
																this.queryBoxLabel)
														.addComponent(
																this.queryBox,
																javax.swing.GroupLayout.PREFERRED_SIZE,
																javax.swing.GroupLayout.DEFAULT_SIZE,
																javax.swing.GroupLayout.PREFERRED_SIZE)
														.addComponent(
																this.searchButton)
														.addComponent(
																this.initButton))
										.addGap(29, 29, 29)
										.addGroup(
												layout
														.createParallelGroup(
																javax.swing.GroupLayout.Alignment.LEADING)
														.addComponent(
																this.resultPanel,
																javax.swing.GroupLayout.Alignment.TRAILING,
																javax.swing.GroupLayout.PREFERRED_SIZE,
																264,
																javax.swing.GroupLayout.PREFERRED_SIZE)
														.addGroup(
																javax.swing.GroupLayout.Alignment.TRAILING,
																layout
																		.createSequentialGroup()
																		.addGroup(
																				layout
																						.createParallelGroup(
																								javax.swing.GroupLayout.Alignment.BASELINE)
																						.addComponent(
																								this.URILabel)
																						.addComponent(
																								this.URIfield,
																								javax.swing.GroupLayout.PREFERRED_SIZE,
																								javax.swing.GroupLayout.DEFAULT_SIZE,
																								javax.swing.GroupLayout.PREFERRED_SIZE))
																		.addPreferredGap(
																				javax.swing.LayoutStyle.ComponentPlacement.RELATED)
																		.addComponent(
																				this.jScrollPane1,
																				javax.swing.GroupLayout.PREFERRED_SIZE,
																				javax.swing.GroupLayout.DEFAULT_SIZE,
																				javax.swing.GroupLayout.PREFERRED_SIZE)
																		.addGap(
																				26,
																				26,
																				26)
																		.addGroup(
																				layout
																						.createParallelGroup(
																								javax.swing.GroupLayout.Alignment.LEADING)
																						.addGroup(
																								layout
																										.createParallelGroup(
																												javax.swing.GroupLayout.Alignment.TRAILING)
																										.addGroup(
																												layout
																														.createSequentialGroup()
																														.addComponent(
																																this.timeLabel)
																														.addGap(
																																18,
																																18,
																																18)
																														.addComponent(
																																this.resultsLable))
																										.addGroup(
																												layout
																														.createSequentialGroup()
																														.addComponent(
																																this.linearLabel)
																														.addGap(
																																18,
																																18,
																																18)
																														.addComponent(
																																this.linearTime)
																														.addGap(
																																18,
																																18,
																																18)
																														.addComponent(
																																this.wordRes)))
																						.addGroup(
																								layout
																										.createSequentialGroup()
																										.addComponent(
																												this.indexedLabel)
																										.addGap(
																												18,
																												18,
																												18)
																										.addComponent(
																												this.indexedTime)
																										.addGap(
																												18,
																												18,
																												18)
																										.addComponent(
																												this.charRes)))))
										.addContainerGap(
												60,
												javax.swing.GroupLayout.PREFERRED_SIZE)));

		this.pack();
	}

	private void queryBoxActionPerformed(final java.awt.event.ActionEvent evt) {
	}

	private void resultListValueChanged(
			final javax.swing.event.ListSelectionEvent evt) {
		try {
			this.URIfield.setText(LoadData.getDocURI(this.resultList
					.getSelectedIndex()));
			this.preview.setText(LoadData.getDocPreview(this.resultList
					.getSelectedIndex()));
		} catch (final Exception e) {
		}
	}

	private void searchButtonActionPerformed(
			final java.awt.event.ActionEvent evt) {
		try {
			LoadData.clear();
			System.out.println("Staring search.");
			LoadData.query = this.queryBox.getText();
			// word index search
			LoadData.searchResults = LoadData
					.wordIndexSearchTFIDF(LoadData.query);
			System.out.println("Found " + LoadData.searchResults.size()
					+ " results.");
			// char index search
			final ArrayList<ResultNode> results = LoadData
					.indexSearch(LoadData.query);
			System.out.println("Found " + results.size() + " results.");

			final ArrayList<String> docIDList = LoadData
					.genResultIDList(LoadData.searchResults);

			this.resultsLable.setText("Results");
			this.wordRes.setText(Integer
					.toString(LoadData.searchResults.size()));
			this.charRes.setText(Integer.toString(results.size()));
			this.linearTime.setText(Double.toString(LoadData.wordSearchTime));
			this.indexedTime.setText(Double
					.toString(LoadData.indexedSearchTime));
			System.out.println("Speedup rate = "
					+ (LoadData.wordSearchTime / LoadData.indexedSearchTime));

			this.resultList.setModel(new javax.swing.AbstractListModel() {

				private static final long serialVersionUID = -2806783116317526960L;

				public Object getElementAt(final int i) {
					return this.strings.get(i);
				}

				public int getSize() {
					return this.strings.size();
				}

				ArrayList<String> strings = docIDList;
			});
		} catch (final Exception e) {
		}
	}

	private void URIfieldActionPerformed(final java.awt.event.ActionEvent evt) {
	}

	private javax.swing.JLabel charRes;
	private javax.swing.JLabel indexedLabel;
	private javax.swing.JLabel indexedTime;
	private javax.swing.JButton initButton;
	private javax.swing.JScrollPane jScrollPane1;
	private javax.swing.JLabel linearLabel;
	private javax.swing.JLabel linearTime;
	private javax.swing.JTextArea preview;
	private javax.swing.JTextField queryBox;
	private javax.swing.JLabel queryBoxLabel;
	private javax.swing.JList resultList;
	private javax.swing.JScrollPane resultPanel;
	private javax.swing.JLabel resultsLable;
	private javax.swing.JButton searchButton;
	private javax.swing.JLabel timeLabel;
	private javax.swing.JTextField URIfield;
	private javax.swing.JLabel URILabel;
	private javax.swing.JLabel wordRes;
}
